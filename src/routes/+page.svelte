<script>
    import PillContainer from '$lib/components/PillContainer.svelte';
</script>

<div class="home-banner">
<PillContainer height="100%" verticalEnergy={0.4} horizontalEnergy={0.6} count={12} speed={1.5} spawnDelay={150}>
    <div class="banner-text">
        <p class='main-text'>Configuring ePrescribing
        systems to keep
        patients safe</p>
		<p class='sub-text'><q>Know your risk: An NHS self-assessment for safer ePrescribing.</q></p>
    </div>
</PillContainer>
</div>

<style>
	.banner-text {
		font-family: "Raleway", sans-serif;
		font-weight: 200;
		color: var(--nhs-blue);
		font-size: clamp(2.5rem, 5vw, 4rem);
		z-index: 10;
		pointer-events: none;
		padding-left: clamp(5%, 10vw, 7%);
		text-shadow: 0 0 20px rgba(255, 255, 255, 0.5);
		animation: fadeUp 0.8s ease-out forwards;
	}

	.banner-text .main-text {
		width: 50%;
		line-height: 1.2;
	}

	.banner-text .sub-text {
		font-size: clamp(1.2rem, 3vw, 2rem);
		margin-top: 0.5em;
		color: var(--nhs-dark-blue);
		text-shadow: 0 0 10px rgba(255, 255, 255, 0.4);
	}

	.home-banner {
		view-transition-name: pill-box;
		position: relative;
		display: flex;
		flex: 1;
		flex-direction: column;
		width: 100%;
		padding: 0;
		margin: 0;
		border-bottom: 1px solid #eee;
		border-top: 1px solid #eee;
		overflow: hidden;
		background-color: #eff3fb;
	}
	
	.home-banner :global(.pill-stage) {
		flex: 1;
		height: 100%;
		width: 100%;
	}
	.home-banner::after {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        /* This sits on top of the pills */
        box-shadow: inset 0 60px 60px -60px rgba(34, 61, 152, 0.15),
					inset 0 -60px 60px -60px rgba(34, 61, 152, 0.15); 
        pointer-events: none; /* Crucial: clicks pass through to the content */
        z-index: 2; 
    }
</style>