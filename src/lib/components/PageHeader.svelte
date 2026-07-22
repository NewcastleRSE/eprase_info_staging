<script lang="ts">
    import PillContainer from './PillContainer.svelte';
    let { title = "Untitled" } = $props();
    let myCount = Math.random() < 0.33 ? 3 : 4; // Randomly choose between 3 and 4 pills for some variety
</script>

<div class="subpage-wrapper">
<header class="subpage-header">
    <PillContainer height="100%" minSize={25} maxSize={50} count={myCount} speed={0.4} spawnDelay={400} leftWallPercent={0.75} verticalEnergy={0.5}>
        <div class="header-content">
            <h1>{title}</h1>
        </div>
    </PillContainer>
</header>
</div>

<style>
    .subpage-wrapper {
        view-transition-name: pill-box;
        display: flex;
        width: 100%;
        height: clamp(80px, 12vmin, 150px);
        background-color: #eff3fb;
        box-shadow: inset 0 0 20px rgba(34, 61, 152, 0.1);
    }

    .subpage-wrapper :global(.pill-stage) {
		height: 100%;
		width: 100%;
        background: transparent !important;
	}
    .subpage-header {
        position: relative;
        flex: 1;
        width: 100%;
        border-bottom: 1px solid #eee;
        overflow: hidden;
    }

    .subpage-header::after {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        pointer-events: none; 
        z-index: 6; 
    }

    .header-content {
        height: 100%;
        width: 100%;
        display: flex;
        align-items: center;
        padding-left: 5%;
        background: transparent;
    }

    h1 {
        font-family: "Raleway", sans-serif;
        font-weight: 200;
        color: var(--nhs-dark-blue);
        margin: 0;
        font-size: clamp(1.8rem, 3vw, 3.5rem);
        pointer-events: none;
        animation: fadeUp 0.8s ease-out forwards;
        text-shadow: 0 2px 10px rgba(65, 182, 230, 0.4);
    }
</style>