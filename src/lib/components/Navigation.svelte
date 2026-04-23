<script>
    import { page } from '$app/state';
    let isMenuOpen = $state(false);
    const toggleMenu = () => isMenuOpen = !isMenuOpen;
    const closeMenu = () => isMenuOpen = false;
    
    const bottomLinks = [
        { name: 'About', path: '/about' },
        { name: 'Using ePRaSE', path: '/using' },
        { name: 'Results', path: '/results' },
        { name: 'Learning Lab', path: '/lab' }
    ];

    const topLinks = [
        { name: 'News', path: '/news' },
        { name: 'FAQ', path: '/faq' },
        { name: 'Contact', path: 'mailto:nuth.eprase@nhs.net' }
    ];

    const allLinks = bottomLinks.concat(topLinks);
    const isActive = (path) => page.url.pathname.replace(/\/$/, '') === path.replace(/\/$/, '');
</script>
<nav id="topnav">
    <div class="logo-area">
        <a href="/"><img src="/img/classic_logo.png" alt="EPRASE Logo"></a>
    </div>
    <div class="nav-stack">
        <div class="logo-row">
            <img src="/img/nhs.png" class="nhs" alt="NHS"/>
        </div>
        <div class="nav-row top-row desktop-only">
            {#each topLinks as link}
                <a 
                    href={link.path} 
                    class:active={page.url.pathname.replace(/\/$/, '') === link.path.replace(/\/$/, '')}
                    aria-current={page.url.pathname.replace(/\/$/, '') === link.path.replace(/\/$/, '') ? 'page' : undefined}
                >
                    {link.name}
                </a>
            {/each}
            </div>
        <hr class="nav-divider">
        <div class="nav-row bottom-row desktop-only">
            {#each bottomLinks as link}
                <a 
                    href={link.path} 
                    class:active={page.url.pathname.replace(/\/$/, '') === link.path.replace(/\/$/, '')}
                    aria-current={page.url.pathname.replace(/\/$/, '') === link.path.replace(/\/$/, '') ? 'page' : undefined}
                >
                    {link.name}
                </a>
            {/each} 
        </div>
    </div>

    <button class="burger mobile-only" onclick={toggleMenu} aria-label="Toggle Menu">
        <span class:open={isMenuOpen}></span>
        <span class:open={isMenuOpen}></span>
        <span class:open={isMenuOpen}></span>
    </button>

    <div class="mobile-menu" class:open={isMenuOpen}>
        {#each allLinks as link}
            <a href={link.path} onclick={closeMenu} class:active={isActive(link.path)}>
                {link.name}
            </a>
        {/each}
    </div>
</nav>

<style>
    #topnav {
        display: flex;
        justify-content: space-between; /* Pushes logo left, nav right */
        align-items: center;
        height: clamp(80px, 25vmin, 250px);
        padding: clamp(10px, 4vh, 40px) clamp(20px, 5%, 60px);
        font-family: "Raleway", sans-serif;
        position: relative;
        background: linear-gradient(to bottom right, var(--nhs-blue), var(--nhs-dark-blue));
        z-index: 2000;
        opacity: 0.95;
        border-bottom: 1px solid #d1d9e6;
        box-shadow: inset 0 0 20px rgba(34, 61, 152, 0.2);
    }

    .logo-row {
        display: flex;
        justify-content: flex-end;
        width: 100%;
        padding-bottom: 4px; /* Tiny bit of separation from the links */
    }

    .nhs {
        height: clamp(20px, 3vmin, 40px);
        width: auto;
        display: block;
    }

    .nav-stack {
        display: flex;
        flex-direction: column; /* Stacks the two rows vertically */
        align-items: flex-end;   /* Aligns the text to the right edge */
        gap: 8px;               /* Space between rows and line */
        color: #FFFFFF;
    }

    .nav-row a {
        text-decoration: none;
        color: #FFFFFF;
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
    .nav-row a:hover, .bottom-row a.active {
        color: #3498DB; 
        border-color: #3498DB; /* Just reveal the border color */
    }

    /* Top Row Hover Override */
    .top-row a.active, .top-row a:hover {
        background: #3498DB;
        border-color: #3498DB;
        color: #fff;
    }

    /* Adjusting the top-row base size to match your design */
    .top-row a {
        font-size: 1rem;
        opacity: 0.9;
    }
    .nav-row a[aria-current="page"] {
        color: #3498DB; 
        border-color: #3498DB;
        font-weight: 500;
        pointer-events: none;
    }

    .top-row a[aria-current="page"] {
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
    /* Bottom Row Active */
    .bottom-row a.active {
        color: #3498DB; 
        border-color: #3498DB;
        font-weight: 500;
        pointer-events: none;
    }

    /* Top Row Active */
    .top-row a.active {
        background: #3498DB;
        border-color: #3498DB;
        color: #fff;
        opacity: 1;
        pointer-events: none;
    }

    .logo-area img {
        height: clamp(60px, 5vw, 90px);
        width: auto; /* Keeps the proportions perfect */
        transition: filter 0.3s ease; /* Bonus: for a clean hover effect */
    }

    /* MOBILE LOGIC */
    .mobile-only { display: none; }
    .mobile-menu { display: none; }

    @media (max-width: 1024px) {
        .desktop-only { display: none; }
        .mobile-only { display: flex; }

        /* Burger Icon */
        .burger {
            flex-direction: column;
            gap: 6px;
            background: none;
            border: none;
            cursor: pointer;
        }
        .burger span { width: 30px; height: 3px; background: #EEE; transition: 0.3s; }
        .burger span.open:nth-child(1) { transform: translateY(9px) rotate(45deg); }
        .burger span.open:nth-child(2) { opacity: 0; }
        .burger span.open:nth-child(3) { transform: translateY(-9px) rotate(-45deg); }

        /* Actual Mobile Menu */
        .mobile-menu {
            display: flex;
            position: absolute;
            top: 100%;
            left: 0;
            width: 100%;
            flex-direction: column;
            background: white;
            padding: 20px 0;
            border-bottom: 2px solid #eff3fb;
            transform: translateY(-150%);
            transition: transform 0.4s ease-in-out;
            z-index: -1;
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
        }
        .mobile-menu.open { transform: translateY(0); }
        .mobile-menu a:hover {
            color: #3498DB;
        }
        .mobile-menu a {
            padding: 15px;
            text-align: center;
            text-decoration: none;
            color: #171717;
            font-size: 1.2rem;
        }
        .mobile-menu a.active { color: #3498DB; font-weight: bold; }
        .nav-stack {
            flex-direction: column
        }
    }
</style>
