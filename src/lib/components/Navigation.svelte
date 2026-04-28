<script>
    import { page } from '$app/state';
    import { resolve } from '$app/paths';
    
    let isMenuOpen = $state(false);
    const toggleMenu = () => isMenuOpen = !isMenuOpen;
    const closeMenu = () => isMenuOpen = false;
    
    // The helper function for GitHub Pages subdirectories
    const link = (path) => resolve(path);
    
    const bottomLinks = [
        { name: 'About', path: '/about' },
        { name: 'Using ePRaSE', path: '/using' },
        { name: 'Results', path: '/results/2025' },
        { name: 'Learning Lab', path: '/lab' }
    ];

    const topLinks = [
        { name: 'News', path: '/news' },
        { name: 'FAQ', path: '/faq' },
        { name: 'Contact', path: 'mailto:nuth.eprase@nhs.net' }
    ];

    const allLinks = [...bottomLinks, ...topLinks];
    
    // Updated isActive to use resolve for accurate production matching
    const isActive = (path) => page.url.pathname.replace(/\/$/, '') === resolve(path).replace(/\/$/, '');
</script>

<nav id="topnav">
    <div class="logo-area">
        <a href={link('/')}>
            <img src={link('/img/classic_logo.png')} alt="EPRASE Logo">
        </a>
    </div>

    <div class="nav-stack">
        <div class="logo-row">
            <img src={link('/img/nhs.png')} class="nhs" alt="NHS"/>
        </div>

        <div class="nav-row top-row desktop-only">
            {#each topLinks as item}
                <a 
                    href={item.path.startsWith('mailto') ? item.path : link(item.path)} 
                    class:active={isActive(item.path)}
                    aria-current={isActive(item.path) ? 'page' : undefined}
                >
                    {item.name}
                </a>
            {/each}
        </div>

        <hr class="nav-divider desktop-only">

        <div class="nav-row bottom-row desktop-only">
            {#each bottomLinks as item}
                <a 
                    href={link(item.path)} 
                    class:active={isActive(item.path)}
                    aria-current={isActive(item.path) ? 'page' : undefined}
                >
                    {item.name}
                </a>
            {/each} 
        </div>

        <button class="burger mobile-only" onclick={toggleMenu} aria-label="Toggle Menu">
            <span class:open={isMenuOpen}></span>
            <span class:open={isMenuOpen}></span>
            <span class:open={isMenuOpen}></span>
        </button>
    </div>

    <div class="mobile-menu" class:open={isMenuOpen}>
        {#each allLinks as item}
            <a 
                href={item.path.startsWith('mailto') ? item.path : link(item.path)} 
                onclick={closeMenu} 
                class:active={isActive(item.path)}
            >
                {item.name}
            </a>
        {/each}
    </div>
</nav>

<style>
    /* CSS remains exactly as you had it, 
       ensure .nav-stack uses flex-direction: column 
       to keep NHS above the Burger! */
    
    #topnav {
        display: flex;
        justify-content: space-between;
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
        padding-bottom: 4px;
    }

    .nhs {
        height: clamp(20px, 3vmin, 40px);
        width: auto;
        display: block;
    }

    .nav-stack {
        display: flex;
        flex-direction: column;
        align-items: flex-end;
        justify-content: center;
        gap: 8px;
        color: #FFFFFF;
    }

    .nav-row a {
        text-decoration: none;
        color: #FFFFFF;
        font-size: 1.1rem;
        padding: 4px 12px; 
        border: 1px solid transparent; 
        border-radius: 20px;
        transition: all 0.4s ease; 
        display: inline-block;
    }

    .nav-row a:hover, .bottom-row a.active {
        color: #add2eb; 
        border-color: #3498DB;
    }

    .top-row a.active, .top-row a:hover {
        background: #3498DB;
        border-color: #3498DB;
        color: #fff;
    }

    .top-row a {
        font-size: 1rem;
        opacity: 0.9;
    }

    .nav-divider {
        width: 100%;
        border: 0;
        border-top: 1px solid rgba(255, 255, 255, 0.2);
        margin: 4px 0;
    }

    .logo-area img {
        height: clamp(60px, 5vw, 90px);
        width: auto;
    }

    .mobile-only { display: none; }
    .mobile-menu { display: none; }

    @media (max-width: 1024px) {
        .desktop-only { display: none; }
        .mobile-only { display: flex; }

        .burger {
            display: flex;
            flex-direction: column;
            gap: 6px;
            background: none;
            border: none;
            cursor: pointer;
            padding: 0;
        }

        .burger span { width: 30px; height: 3px; background: #EEE; transition: 0.3s; }
        .burger span.open:nth-child(1) { transform: translateY(9px) rotate(45deg); }
        .burger span.open:nth-child(2) { opacity: 0; }
        .burger span.open:nth-child(3) { transform: translateY(-9px) rotate(-45deg); }

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
        .mobile-menu a {
            padding: 15px;
            text-align: center;
            text-decoration: none;
            color: #171717;
            font-size: 1.2rem;
        }
        .mobile-menu a.active { color: #3498DB; font-weight: bold; }

        .nhs { height: 22px; }
    }
</style>