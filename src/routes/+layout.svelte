<script lang="ts">
    import { page } from '$app/state';
    let { children } = $props();
    export const prerender = true;
    let menuOpen = $state(false);

    const bottomLinks = [
        { name: 'About', path: '/about' },
        { name: 'Using ePRaSE', path: '/using' },
        { name: 'Results', path: '/results' },
        { name: 'Learning Lab', path: '/lab' }
    ];

    const topLinks = [
        { name: 'News', path: '/news' },
        { name: 'FAQ', path: '/faq' },
        { name: 'Contact', path: '/contact' }
    ];

    const allLinks = bottomLinks.concat(topLinks);

</script>
<nav id="topnav">
    <div class="logo-area">
        <a href="/"><img src="img/eprase_logo_color.png" alt="EPRASE Logo"></a>
    </div>
    <div class="nav-stack">
        <div class="nav-row top-row desktop-only">
            {#each topLinks as link}
                <a href={link.path} 
                aria-current={page.url.pathname === link.path ? 'page' : undefined} >
                {link.name}
                </a>
            {/each}
            </div>
            <hr class="nav-divider">
        <div class="nav-row bottom-row desktop-only">
            {#each bottomLinks as link}
                <a href={link.path} 
                aria-current={page.url.pathname === link.path ? 'page' : undefined} >
                {link.name}
                </a>
            {/each} 
        </div>
    </div>
</nav>
<main>
    {@render children()}
</main>

<footer><img src="img/ncl_logo.png" alt="NCL Logo"><img src="img/nhs_logo.png" alt="NHS Logo"></footer>

<style>
     /* --- SHARED STYLES --- */
    @property --color1 { syntax: '<color>'; initial-value: #2C3E50; inherits: true; }
    @property --color2 { syntax: '<color>'; initial-value: #BDC3C7; inherits: true; }
    #topnav {
        display: flex;
        justify-content: space-between; /* Pushes logo left, nav right */
        align-items: center;
        padding: 0 40px;
        height: 150px;
        font-family: "Raleway", sans-serif;
    }

    .nav-stack {
        display: flex;
        flex-direction: column; /* Stacks the two rows vertically */
        align-items: flex-end;   /* Aligns the text to the right edge */
        gap: 8px;               /* Space between rows and line */
    }

    .nav-row a {
        text-decoration: none;
        color: #171717;
        font-size: 1.1rem;
        
        /* 1. Pre-apply the spacing so it never shifts */
        padding: 4px 12px; 
        border: 1px solid transparent; 
        border-radius: 20px;
        
        /* 2. Smoothly transition everything */
        transition: all 0.4s ease; 
        display: inline-block; /* Ensures padding/height are respected */
    }

    /* Bottom Row Hover */
    .nav-row a:hover {
        color: #3498DB; 
        border-color: #3498DB; /* Just reveal the border color */
    }

    /* Top Row Hover Override */
    .top-row a:hover {
        background: #3498DB;
        border-color: #3498DB;
        color: #fff;
    }

    /* Adjusting the top-row base size to match your design */
    .top-row a {
        font-size: 1rem;
        opacity: 0.9;
    }
    .nav-row a[aria-current="true"] {
        color: #3498DB; 
        border-color: #3498DB;
        font-weight: 500;
        pointer-events: none;
    }

    .top-row a[aria-current="true"] {
        background: #3498DB;
        color: #fff;
        opacity: 1;
    }

    .nav-divider {
        width: 100%;            /* Line spans the width of the link stack */
        border: 0;
        border-top: 1px solid #666;
        margin: 4px 0;
    }
    .logo-area img {
        height: 80px;           /* Adjust logo size as needed */
    }

    footer {
        /* The Magic Math */
        height: calc(25vh - 150px); 
        
        /* Layout */
        display: flex;
        justify-content: center; /* Centers logos horizontally */
        align-items: center;     /* Centers logos vertically */
        gap: 100px;               /* Space between the two logos */
        
        background-color: #fff;
        padding: 20px 0;
        box-sizing: border-box;  /* Ensures padding doesn't add to height */
    }

    footer img {
        height: 60px;            /* Consistent height for partner logos */
        filter: grayscale(40%);
        opacity: 0.8;
        transition: all 0.3s ease;
    }

    footer img:hover {
        filter: grayscale(0%);
        opacity: 1;
    }

    /** global styles */
    :global(body) { 
        margin: 0; 
        padding: 0; 
        background: #fff; 
        overflow-x: hidden; 
        display: flex;
        flex-direction: column;
        height: 100vh;
    }
    


</style>