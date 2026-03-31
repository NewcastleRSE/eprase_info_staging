<script lang="ts">
	import { onMount } from 'svelte';

    // 1. Props
    let { 
        height = "75vh",
        count = 12, 
        speed = 1.5, 
        horizontalEnergy = 0.4,
        verticalEnergy = 0.4,
        pulseSpeed = 0.003,
        pulseRange = 0.12,
        minSize = 35,
        maxSize = 90,
        minBlur = 2.5,
        maxBlur = 7,
        minOpacity = 0.15,
        maxOpacity = 0.45,
        maxSpin = 0.1
    } = $props();

    // 2. State & Bindings
    let container: HTMLElement;
    let w = $state(0); //div width
    let h = $state(0); //div height
    let balls = $state([]); 

    const colors = ["#2C3E50", "#3498DB", "#16A085", "#218C74"];
    const capMap = {"#2C3E50":"#95a5a6", "#3498DB":"#D1D9E6", "#16A085":"#A3E4D7", "#218C74":"#BDC3C7"};

    onMount(() => {
            
        // Use a small timeout to ensure the browser has calculated 'w' and 'h'
        setTimeout(() => {
            const leftWall = w < 768 ? w * 0.20 : w * 0.33;
            const spawnWidth = w - leftWall - 150; // Total available space on the right
            
            // Initialize the balls using the current width/height
            balls = Array.from({ length: count }, () => {
                const pillColor = colors[Math.floor(Math.random() * colors.length)];
                const isTablet = Math.random() > 0.7;
                const size = minSize + Math.random() * (maxSize - minSize);
                
                return {
                    x: leftWall + (Math.random() * spawnWidth),
                    y: Math.random() * (h - 80),
                    vx: (Math.random() - 0.5) * horizontalEnergy,
                    vy: (Math.random() - 0.5) * verticalEnergy,
                    size: size,
                    phase: Math.random() * Math.PI * 2,
                    rotation: Math.random() * 360,
                    rotationSpeed: (Math.random() - 0.5) * 0.2,
                    color1: pillColor,
                    color2: isTablet ? pillColor : (capMap[pillColor] || "#BDC3C7"),
                    isTablet,
                    scale: 1,
                    baseScale: 1,
                    opacity: 0.3
                };
            });

            loop();
        }, 100);

        let frame: number;
        function loop() {
            // Skip if dimensions aren't ready
            if (w === 0 || h === 0) {
                frame = requestAnimationFrame(loop);
                return;
            }

            // Define the Left Wall: 33% of width on desktop, 20% on mobile
            const leftWall = w < 768 ? w * 0.20 : w * 0.33;
            const rightWall = w - 60; // The invisible "Right Wall" for the anchor point
            // Update every ball in the state
            balls.forEach(b => {
                b.x += b.vx * speed;
                b.y += b.vy * speed;

                // Use a conservative "Safe Width" (The max a pill can ever be)
                const safeWidth = b.size * 2.2; 
                const leftWall = w < 768 ? w * 0.20 : w * 0.33;
                const rightWallLimit = w - safeWidth;
                const floorLimit = h - b.size;

                let hit = false;

                // --- HORIZONTAL BOUNCE ---
                if (b.x <= leftWall) { 
                    b.x = leftWall; 
                    b.vx = Math.abs(b.vx); 
                    hit = true;
                } else if (b.x >= rightWallLimit) { 
                    b.x = rightWallLimit; 
                    b.vx = -Math.abs(b.vx); 
                    hit = true;
                }
                
                // --- VERTICAL BOUNCE ---
                if (b.y <= 0) { 
                    b.y = 0; 
                    b.vy = Math.abs(b.vy); 
                    hit = true;
                } else if (b.y >= floorLimit) { 
                    b.y = floorLimit; 
                    b.vy = -Math.abs(b.vy); 
                    hit = true;
                }

                if (hit) {
                    const newColor = colors[Math.floor(Math.random() * colors.length)];
                    b.color1 = newColor;
                    if (Math.random() < 0.3) b.isTablet = !b.isTablet;
                    b.color2 = b.isTablet ? newColor : (capMap[newColor] || "#BDC3C7");
                    b.rotationSpeed = Math.max(Math.min(b.rotationSpeed + (Math.random() - 0.5) * 0.05, maxSpin), -maxSpin);
                }

                b.rotation += b.rotationSpeed * speed;
                b.phase += pulseSpeed;
                b.scale = 1 + (Math.sin(b.phase) * pulseRange);// Reduced scale range for calmness
                const progress = (b.scale - (1 - pulseRange)) / (pulseRange * 2);
                b.blur = maxBlur - (progress * (maxBlur - minBlur));
                b.opacity = minOpacity + (progress * (maxOpacity - minOpacity));
            });

            // Re-assign to trigger Svelte 5 reactivity
            balls = balls; 
            frame = requestAnimationFrame(loop);
        }

        return () => cancelAnimationFrame(frame);
    });
</script>

<div 
    class="pill-stage" 
    style="height: {height};" 
    bind:this={container}
    bind:clientWidth={w}
    bind:clientHeight={h}
>
    {#each balls as b}
        <div 
            class="ball" 
            class:tablet={b.isTablet}
            style:transform="translate({b.x}px, {b.y}px) scale({b.scale}) rotate({b.rotation}deg)"
            style:opacity={b.opacity}
            style:filter="blur({b.blur}px)"
            style:--size="{b.size}px"
            style:--color1={b.color1}
            style:--color2={b.color2}
        ></div>
    {/each}
    <div class="content-overlay">
        <slot />
    </div>
</div>

<style>
    .pill-stage {
        position: relative;
        width: 100%;
        overflow: hidden;
        background-color: #eff3fb;
    }
    .content-overlay {
        position: absolute; /* Absolute so it sits precisely over the animation */
        top: 0; left: 0;
        z-index: 10;
        pointer-events: none;
        width: 100%;
        height: 100%;
        display: flex;
        align-items: center;
    }

    .ball {
      position: absolute;
      background: linear-gradient(90deg, var(--color1) 50%, var(--color2) 50%);
      z-index: 5;
      will-change: transform, opacity, width, border-radius, filter;
      pointer-events: none;
      transform-origin: center center;
      height: var(--size);
      width: calc(var(--size) * 2.2);
      border-radius: 100px;

      transition:
        width 2s cubic-bezier(0.4, 0, 0.2, 1),
        border-radius 3s cubic-bezier(0.4, 0, 0.2, 1),
        --color1 3s ease,
        --color2 3s ease;
    }

    .ball::after {
      content: '';
      position: absolute;
      top: 50%; left: 0;
      width: 100%; height: 4px;
      background: var(--color1);
      mix-blend-mode: multiply;
      opacity: 0;
      transform: translateY(-50%);
      transition: opacity 0.3s ease;
    }
    .ball.tablet::after { opacity: 0.4; transition: opacity 2s ease 1s;}
    .ball.tablet { border-radius: 50%; width: var(--size); }
    .ball:not(.tablet) { border-radius: 100px; }
</style>