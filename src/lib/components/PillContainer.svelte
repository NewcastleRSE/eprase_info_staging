<script lang="ts">
	import { onMount } from 'svelte';

    // 1. Props
    let { 
        height = "75vh",
        count = 12, 
        speed = 1.5, 
        horizontalEnergy = 0.4
    } = $props();

    // 2. State & Bindings
    let container: HTMLElement;
    let w = $state(0); // This was missing!
    let h = $state(0); // This was missing!
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
                const size = 40 + Math.random() * 40;
                
                return {
                    x: leftWall + (Math.random() * spawnWidth),
                    y: Math.random() * (h - 80),
                    vx: (Math.random() - 0.5) * horizontalEnergy,
                    vy: (Math.random() - 0.5) * 0.4,
                    size: size,
                    phase: Math.random() * Math.PI * 2,
                    rotation: Math.random() * 360,
                    rotationSpeed: (Math.random() - 0.5) * 0.2,
                    color1: pillColor,
                    color2: isTablet ? pillColor : (capMap[pillColor] || "#BDC3C7"),
                    isTablet,
                    scale: 1,
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

                const maxWidth = b.size * 2.2;
                const currentWidth = b.isTablet ? b.size : b.size * 2.2;
                let hit = false;

                // Bounce logic: horizontal
                if (b.x <= leftWall) { 
                    b.x = leftWall; 
                    b.vx = Math.abs(b.vx); 
                    hit = true;
                } else if (b.x >= rightWall) { 
                    b.x = rightWall; 
                    b.vx = -Math.abs(b.vx); 
                    hit = true;
                }
                
                // Bounce logic: vertical
                if (b.y <= 0) { 
                    b.y = 0; 
                    b.vy = Math.abs(b.vy); 
                    hit = true;
                } else if (b.y >= h - b.size) { 
                    b.y = h - b.size; 
                    b.vy = -Math.abs(b.vy); 
                    hit = true;
                }

                // --- IMPACT EFFECTS --- 
                if (hit) {
                    //color shift
                    const newColor = colors[Math.floor(Math.random() * colors.length)];
                    b.color1 = newColor;

                    //shape shift
                    if(Math.random() < 0.3) {
                        b.isTablet = !b.isTablet;                        
                    }

                    //cap color based on new shape/color
                    b.color2 = b.isTablet ? newColor : (capMap[newColor] || "#BDC3C7");
                    b.rotationSpeed += (Math.random() - 0.5) * 0.05; 
                    // set a max rotation speed
                    b.rotationSpeed = Math.max(Math.min(b.rotationSpeed, 0.2), -0.2);
                    
                }
                b.rotation += b.rotationSpeed * speed;
                b.phase += 0.005;
                b.scale = 1 + (Math.sin(b.phase) * 0.2);
                b.blur = 10 - (b.scale * 6.5);
                b.opacity = 0.2 + (b.scale * 0.25);
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
      top: 0; left: 0;
      pointer-events: none;

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