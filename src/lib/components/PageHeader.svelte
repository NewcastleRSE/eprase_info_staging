<script lang="ts">
    import PillContainer from './PillContainer.svelte';
    let { title = "Untitled" } = $props();
    let myCount = Math.random() < 0.33 ? 3 : 4; // Randomly choose between 3 and 4 pills for some variety
</script>

<div class="subpage-wrapper">
<header class="subpage-header">
    <PillContainer height="100%" count={myCount} speed={0.4} spawnDelay={400} leftWallPercent={0.75} verticalEnergy={0.5}>
        <div class="header-content">
            <h1>{title}</h1>
        </div>
    </PillContainer>
</header>
</div>

<style>
    .subpage-wrapper {
        width: 100%;
        display: flex;
        height: clamp(10vh, 25vh, 20vh);
    }

    .subpage-wrapper :global(.pill-stage) {
		height: 100%;
		width: 100%;
	}
    .subpage-header {
        position: relative;
        width: 100%;
        border-bottom: 1px solid #eee;
        border-top: 1px solid #eee;
        overflow: hidden;
    }

    .subpage-header::after {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        /* This sits on top of the pills */
        box-shadow: inset 0 0 60px rgba(34, 61, 152, 0.15); 
        pointer-events: none; /* Crucial: clicks pass through to the content */
        z-index: 2; 
    }

    .header-content {
        height: 100%;
        width: 100%;
        z-index: 3;
        display: flex;
        align-items: center;
        padding-left: 5%; 
    }

    h1 {
        font-family: "Raleway", sans-serif;
        font-weight: 200;
        color: #474747;
        margin: 0;
        font-size: clamp(2rem, 5vw, 3.5rem);
        pointer-events: none;
        text-shadow: 0 2px 10px rgba(255, 255, 255, 0.5);
        animation: fadeUp 0.8s ease-out forwards;
    }
</style>