<script>
    import PillContainer from '$lib/components/PillContainer.svelte';
</script>

<PillContainer height="75vh" count={12} speed={1.5}>
    <div class="banner-text">
        Configuring e-prescribing<br>
        systems to keep<br>
        patients safe
    </div>
</PillContainer>

<style>
	.banner-text {
		font-family: "Raleway", sans-serif;
		font-weight: 200;
		color: #474747;
		font-size: 4rem;
		z-index: 10;
		pointer-events: none;
		padding-left: 5%;
		text-shadow: 0 0 20px rgba(255, 255, 255, 0.5);
	}
</style>