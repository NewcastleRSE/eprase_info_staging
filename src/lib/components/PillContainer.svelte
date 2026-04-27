<script lang="ts">
    import { onMount } from 'svelte';

    let { 
        height = "75vh",
        count = 12, 
        leftWallPercent = 0.33,
        minLargeCount = 6,
        heroSizeMin = 70,
        speed = 1.5, 
        horizontalEnergy = 0.4,
        verticalEnergy = 0.4,
        minPulseSpeed = 0.001,
        maxPulseSpeed = 0.005,
        pulseRange = 0.12,
        minSize = 35,
        maxSize = 90,
        minBlur = 2,
        maxBlur = 7,
        minOpacity = 0.15,
        maxOpacity = 0.45,
        maxSpin = 0.1,
        spawnDelay = 300,
        children
    } = $props();

    let w = $state(0);
    let h = $state(0);
    let balls = $state([]); 
    let activeMinSize = $derived(w > 0 && w <= 768 ? 25 : minSize);
    let activeMaxSize = $derived(w > 0 && w <= 768 ? 60 : maxSize);
    let activeHeroSizeMin = $derived(w > 0 && w <= 768 ? 50 : heroSizeMin);

    let stageReady = $derived(w > 0 && h > 0);

    const colors = ["#009460", "#00BC7A", "#00396F", "#3498DB"];
    const capMap = {
        "#009460": "#CDE6DB", // Deepened Sage
        "#00BC7A": "#C5EDDC", // Deepened Mint
        "#00396F": "#CFD9E1", // Deepened Steel Blue
        "#3498DB": "#D1E6F3"  // Deepened Sky Blue
    };
    let safeWidth = $derived(activeMaxSize * 2.2);
    let leftWall = $derived(w <= 768 ? w * 0.40 : w * leftWallPercent);
    let rightWallLimit = $derived(w - safeWidth);

    let frame: number;

    function loop() {
        if (stageReady && balls.length > 0) {
            balls.forEach(b => {
                b.x += b.vx * speed;
                b.y += b.vy * speed;
                const floorLimit = h - b.size;
                let hit = false;
                
                if (b.x <= leftWall) { b.x = leftWall; b.vx = Math.abs(b.vx); hit = true; }
                else if (b.x >= rightWallLimit) { b.x = rightWallLimit; b.vx = -Math.abs(b.vx); hit = true; }
                
                if (b.y <= 0) { b.y = 0; b.vy = Math.abs(b.vy); hit = true; }
                else if (b.y >= floorLimit) { b.y = floorLimit; b.vy = -Math.abs(b.vy); hit = true; }

                if (hit) {
                    const otherColors = colors.filter(c => c !== b.color1);
                    const newColor = otherColors.length > 0 ? otherColors[Math.floor(Math.random() * otherColors.length)] : b.color1;
                    b.color1 = newColor;
                    if (Math.random() < 0.3) b.isTablet = !b.isTablet;
                    b.color2 = b.isTablet ? newColor : (capMap[newColor] || "#BDC3C7");
                    b.rotationSpeed = Math.max(Math.min(b.rotationSpeed + (Math.random() - 0.5) * 0.05, maxSpin), -maxSpin);
                }

                b.rotation += b.rotationSpeed * speed;
                b.phase += b.myPulseSpeed;
                b.scale = 1 + (Math.sin(b.phase) * pulseRange);
                const physicalSize = b.size * b.scale;
                const progress = Math.max(0, Math.min(1, (physicalSize - minSize) / (maxSize - minSize)));
                const curvedProgress = Math.pow(progress, 2); //won't get too blurry too fast
                b.blur = maxBlur - (curvedProgress * (maxBlur - minBlur));
                b.opacity = minOpacity + (curvedProgress * (maxOpacity - minOpacity));
            });
        }
        frame = requestAnimationFrame(loop);
    }

    onMount(() => {
        let spawned = 0;
        let interval: ReturnType<typeof setInterval>;

        // CRITICAL FIX: The Waiting Room
        // We don't start the 'spawnDelay' interval until w and h are real numbers
        const checkDims = setInterval(() => {
            if (w > 0 && h > 0) {
                clearInterval(checkDims);
                
                interval = setInterval(() => {
                    if (spawned >= count) {
                        clearInterval(interval);
                        return;
                    } 

                    const progress = count > 1 ? spawned / (count - 1) : 0;
                    
                    // We now use the 'real' w and h which are guaranteed to be > 0
                    const startX = leftWall + (progress * (w - leftWall - safeWidth)); 
                    const startY = (h * 0.1) + (progress * (h * 0.6)); 
                    
                    const startColor = colors[Math.floor(Math.random() * colors.length)];
                    let finalSize = (spawned < minLargeCount) 
                        ? activeHeroSizeMin + Math.random() * (activeMaxSize - activeHeroSizeMin)
                        : activeMinSize + Math.random() * (activeMaxSize - activeMinSize);

                    const newPill = {
                        x: startX,
                        y: startY,
                        vx: (0.1 + Math.random() * 0.5) * horizontalEnergy,
                        vy: (0.1 + Math.random() * 0.5) * verticalEnergy,
                        size: finalSize,
                        phase: Math.random() * Math.PI * 2,
                        rotation: Math.random() * 360,
                        rotationSpeed: (Math.random() - 0.5) * maxSpin,
                        color1: startColor,
                        color2: capMap[startColor] || "#BDC3C7",
                        isTablet: Math.random() > 0.7,
                        scale: 1,
                        opacity: maxOpacity,
                        myPulseSpeed: minPulseSpeed + Math.random() * (maxPulseSpeed - minPulseSpeed),
                    };
                    
                    balls = [...balls, newPill];
                    spawned++;
                }, spawnDelay);
            }
        }, 30); // Check every 30ms for dimensions

        loop();

        return () => {
            clearInterval(checkDims);
            if (interval) clearInterval(interval);
            cancelAnimationFrame(frame);
        };
    });
</script>

<div 
    class="pill-stage" 
    style="height: {height}; background: transparent;" 
    bind:clientWidth={w}
    bind:clientHeight={h}
>
    {#each balls as b}
        <div 
            class="ball" 
            class:tablet={b.isTablet}
            style:transform="scale({b.scale}) rotate({b.rotation}deg)"
            style:left="{b.x}px"
            style:top="{b.y}px"
            style:opacity="{b.opacity}"
            style:filter="blur({b.blur}px)"
            style:--size="{b.size}px"
            style:--color1="{b.color1}"
            style:--color2="{b.color2}"
        >
            <div class="cap"></div>
        </div>
    {/each}
    <div class="content-overlay">
        {@render children()}
    </div>
</div>

<style>
    @keyframes pill-entrance {
    from { 
        opacity: 0; 
        transform: scale(0.5) rotate(-20deg); 
    }
    to { 
        /* The inline styles from the loop will take over from here */
    }
}
    .pill-stage {
        position: relative;
        width: 100%;
        overflow: hidden;
        background: transparent;
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
      background-color: var(--color2);
      z-index: 5;
      will-change: transform, opacity, width, border-radius, filter;
      pointer-events: none;
      transform-origin: center center;
      height: var(--size);
      width: calc(var(--size) * 2.2);
      border-radius: 100px;
      overflow: hidden;

      transition:
        width 2s cubic-bezier(0.4, 0, 0.2, 1),
        border-radius 3s cubic-bezier(0.4, 0, 0.2, 1),
        background-color 2s ease;

      animation: pill-entrance 0.8s cubic-bezier(0.2, 0, 0.2, 1) forwards;
    }

    .cap {
        position: absolute;
        top: 0; left: 0;
        height: 100%;
        /* The cap color (Left Side) */
        width: 50%; 
        background-color: var(--color1);
        transition: width 2s cubic-bezier(0.4, 0, 0.2, 1), background-color 2s ease;
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
      z-index: 2;
    }
    .ball.tablet::after { opacity: 0.4; transition: opacity 2s ease 1s;}
    .ball.tablet { border-radius: 50%; width: var(--size); background-color: var(--color1);}
    .ball:not(.tablet) { border-radius: 100px; }
    .ball.tablet .cap {
        width: 100%; /* Cap expands to fill the circle */
    }
    
</style>