<script>
    let { transparent = false } = $props();
</script>

<footer class:home-style={transparent}><img src="/img/ncl_logo.png" alt="NCL Logo"><img src="/img/nhs_logo.png" alt="NHS Logo"></footer>

<style>

    footer {
        min-height: clamp(60px, 10vh, 100px);
        display: flex;
        justify-content: center; /* Centers logos horizontally */
        align-items: center;     /* Centers logos vertically */
        gap: 100px;               /* Space between the two logos */
        width: 100%;
        background-color: linear-gradient(to bottom #eff3fb var(--nhs-light-blue)); /* That clinical light blue/grey */
        border-top: 1px solid #d1d9e6;
        box-shadow: inset 0 0 20px rgba(34, 61, 152, 0.2);
        padding: 20px 0 10px 0;
        overflow: hidden;
        transition: background-color 0.5s ease;
        overflow: hidden;
    }

    footer.home-style {
        background-color: #ffffff;
        box-shadow: none;
        border: none;
    }

    footer img {
        height: clamp(40px, 6vh, 60px);            /* Consistent height for partner logos */
        filter: grayscale(40%);
        opacity: 0.8;
        transition: all 0.3s ease;
    }

    footer img:hover {
        filter: grayscale(0%);
        opacity: 1;
    }
</style>