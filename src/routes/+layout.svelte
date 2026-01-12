<script lang="ts">
    import { page } from '$app/state';
    import { slide } from 'svelte/transition';
    let { children } = $props();
    export const prerender = true;
    let menuOpen = $state(false);

    const navLinks = [
        { name: 'Home', path: '/' },
        { name: 'About', path: '/about' },
        { name: 'Using ePRaSE', path: '/using' },
        { name: 'Results', path: '/results' },
        { name: 'News', path: '/news' },
        { name: 'Learning Lab', path: '/lab' },
        { name: 'FAQ', path: '/faq' }
    ];
</script>
<header id="eprase-header">
    <button title="burger button" id="burger" 
    onclick={() => menuOpen = !menuOpen}
    class="fa {menuOpen ? 'fa-times' : 'fa-bars'}"></button>
</header>

{#if menuOpen}
    <nav class="navbar mobile-only" transition:slide={{ duration: 400, axis: 'y' }}>
        <a href="https://eprase.nhs.uk" class="mynav mobilenav">Sign up now</a>
        {#each navLinks as link}
            <a href={link.path} 
               aria-current={page.url.pathname === link.path} 
               class="mynav mobilenav"
               onclick={() => menuOpen = false}> {link.name}
            </a>
        {/each}
    </nav>
{/if}

<nav class="navbar desktop-only">
    <a href="https://eprase.nhs.uk" class="go2button">Sign up now</a>
    {#each navLinks as link}
        <a href={link.path} 
           aria-current={page.url.pathname === link.path} 
           class="mynav">
           {link.name}
        </a>
    {/each}
</nav>

<main>
    {@render children()}
</main>

<footer class="row w3-center footer">
	<div class='col col-4'><img class='floatleft' src='/img/ncl_logo.png' alt='Newcastle University'></div>
	<div class='col col-4 footercenter'>
  		<p class="eprase-contact"><a href="mailto:nuth.eprase@nhs.net">Contact</a></p>
  	</div>
  	<div class='col col-4 floatright'><img src='/img/nhs_logo.png' alt='NHS England'></div>
</footer>

<style>
     /* --- SHARED STYLES --- */
    :global(body) {margin: 0; font-family:Arial, Helvetica, sans-serif; line-height: 1.5;}
    :global(h1,h2,h3,h4,h5,h6){font-family:"Segoe UI",Arial,sans-serif;font-weight:400;margin:10px 0;}
    :global(.accordion-text) {width: 60%; margin: auto; font-size: 1.2em; line-height: 1.6; margin-bottom: 30px;}
    :global(.eprase-image) {width: 40%; float: right; margin: 0 0 10px 10px; border: 2px solid #1e2a71;}
    :global(.eprase-h1) {font-size: 2.5em; color: #1e2a71; margin-left: 5%; position:relative;animation:animateleft 0.4s}@keyframes animateleft{from{left:-300px;opacity:0} to{left:0;opacity:1}}
    :global(.eprase-h2) {font-size: 1.8em; color: #3e53cc; font-style: italic; margin-left: 15%}
    
    .navbar {
        padding: 0; 
        width: 100%;
        color: #fff !important; 
        background-image: linear-gradient(#3e53cc,#151E51) !important;
    }

    /* Links base style */
    .mynav {
        padding: 16px;
        display: inline-block;
        text-decoration: none;
        color: white !important; /* Force color immediately */
        text-align: center;
        cursor: pointer;
        transition: background 0.2s;
    }

    .mynav:hover, .mynav[aria-current="true"] {
        color: black !important; 
        background-color: #9eb4e6 !important;
    }

    /* --- MOBILE-SPECIFIC --- */
    #burger { 
        display: inline-block; 
        position: absolute;
        bottom: 15px; 
        right: 20px; 
        z-index: 100;
        font-size: 28px!important;
        color: #000;
        background-color: #89aadc;
        border: none;
        margin-bottom: 4px;
        border-radius: 4px;
        padding: 8px 16px;
        vertical-align: middle;
        overflow: hidden;
        text-decoration: none;
        text-align: center;
        cursor: pointer;
        white-space: nowrap;
    }
    #burger:hover {
        color:#000!important;
        background-color:#bccfec!important;
    }

    /* Override for mobile links */
    .mobilenav {
        display: block;
        width: 100%;
        border-bottom: 1px solid rgba(255,255,255,0.1);
        box-sizing: border-box;
    }

    @media (max-width: 768px) {
        #burger { display: block; }
        .desktop-only { display: none !important; }
        
        .navbar.mobile-only {
            display: block; /* Svelte handles visibility via {#if} */
            text-align: center;
        }

        .go2button {
            float: none;
            display: block;
            width: 80%;
            margin: 15px auto;
            text-align: center;
        }
    }

    /* --- DESKTOP-SPECIFIC --- */
    @media (min-width: 769px) {
        .desktop-only { display: block; }
        #burger { display: none; }
    }

    /* --- BANNER & REST --- */
    #eprase-header {
        background-image: url(/img/banner.jpg);
        background-size: cover;
        background-position: center;
        position: relative;
        width: 100%;
        padding-top: 20%;
    }

    .go2button {
        float: right; 
        margin: 10px; 
        background-color: #9aa6e9;
        padding: 8px;
        border-radius: 12px;
        color: #222e66;
        text-decoration: none;
    }
    .go2button:hover {
        background-color: #bccfec;
        color: #000;
        text-decoration: none;
    }
    
    /* Global helpers for the footer/content */
    .row {width: 100%; display: table; text-align: center;}
    .col {display: table-cell; width: 33.33%; float: left;}
    .footer { padding: 16px; background-image:linear-gradient(#bfc6ee, #3e53cc) !important; color: white; }
</style>