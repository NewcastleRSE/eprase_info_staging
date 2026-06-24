<script>
    let { transparent = false } = $props();
    import { resolve } from '$app/paths';
    const link = (path) => resolve(path);
</script>

<footer class:home-style={transparent}>
    <img src={link("/img/logos/nuth.png")} alt="NUTH Logo">
    <img src={link("/img/logos/northumbria.png")} alt="Northumbria Hospitals Logo">
    <img src={link("/img/logos/nppg_logo.png")} alt="NPPG Logo">
    <img src={link("/img/logos/ncl_logo.png")} alt="NCL Logo">
    <img src={link("/img/logos/nhs_logo.png")} alt="NHS Logo">
</footer>

<style>

    footer {
        min-height: clamp(60px, 10vh, 100px);
        display: flex;
        justify-content: center; 
        align-items: center;  
        
        flex-wrap: wrap;         /* Allows logos to drop to the next line on small screens */
        gap: clamp(1.5rem, 4vw, 4rem); /* Dynamic spacing that shrinks on smaller screens */
        padding: 20px 1.5rem; 
        
        width: 100%;
        background: linear-gradient(to bottom, #eff3fb, #eef4fc); 
        border-top: 1px solid #d1d9e6;
        box-shadow: inset 0 0 20px rgba(34, 61, 152, 0.05);
        transition: background-color 0.5s ease;
    }

    footer.home-style {
        background: #ffffff;
        box-shadow: none;
        border: none;
    }

    footer img {
        /* 2. SCALE LOGOS FOR DENSITY */
        height: clamp(35px, 5vh, 50px); 
        width: auto;                   
        object-fit: contain; 
        
        filter: grayscale(60%);
        opacity: 0.75;
        transition: all 0.3s ease;
    }

    footer img:hover {
        filter: grayscale(0%);
        opacity: 1;
    }

    /* 3. MOBILE SPECIFIC TWEAKS */
    @media (max-width: 600px) {
        footer {
            padding: 25px 1rem;
            gap: 1.5rem 2rem; /* Tight row gap, comfortable column gap when stacked */
        }
        
        footer img {
            height: 32px; /* Fixed concise height on small phones so they grid up tightly */
        }
    }
</style>