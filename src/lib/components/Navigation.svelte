<script lang="ts">
    import { page } from '$app/state';
    import { resolve } from '$app/paths';
    
    let isMenuOpen = $state(false);
    let mobileUsingOpen = $state(false);
    let mobileVideosOpen = $state(false);

    const toggleMenu = () => isMenuOpen = !isMenuOpen;
    const closeMenu = () => {
        isMenuOpen = false;
        mobileUsingOpen = false;
        mobileVideosOpen = false;
    };
    
    const link = (path: string) => resolve(path);
    
    // Bottom primary links ('Using ePRaSE' becomes a dropdown container instead of a direct link)
    const bottomLinks = [
        { name: 'About', path: '/about' },
        { name: 'Using ePRaSE', path: '/using', isDropdown: true },
        { name: 'Results', path: '/results/2025' },
        { name: 'Learning Lab', path: '/lab' }
    ];

    // FAQ moved into the "Using ePRaSE" structure as requested
    const topLinks = [
        { name: 'News', path: '/news' },
        { name: 'Contact', path: 'mailto:nuth.eprase@nhs.net' }
    ];

    // Flat mapping list used strictly for simple mobile fallback iteration
    const mobileLinks = [
        { name: 'About', path: '/about' },
        { name: 'Results', path: '/results/2025' },
        { name: 'Learning Lab', path: '/lab' },
        ...topLinks
    ];

    // Sub-navigation hierarchy for the Mega-Menu
    const usingSubLinks = [
        { name: 'FAQ', path: '/using/faq' },
        { name: 'Step-by-step instructions', path: '/using/instructions' },
        { name: 'Video walk-through', path: '/using/walk-through' },
        { name: 'Masterclass presentation', path: '/using/masterclass' },
    ];

    const uxVideos = [
        { name: 'User Experience Video 1', path: '/using/ux-video-1' },
        { name: 'User Experience Video 2', path: '/using/ux-video-2' }
    ];
    
    // Route validation checks
    const isActive = (path: string) => page.url.pathname.replace(/\/$/, '') === resolve(path).replace(/\/$/, '');
    const isSectionActive = (path: string) => page.url.pathname.split('/')[1] === path.split('/')[1];
</script>

<nav id="topnav">
    <div class="logo-area">
        <a href={link('/')} onclick={closeMenu}>
            <img src={link('/img/classic_logo.png')} alt="EPRASE Logo">
        </a>
    </div>

    <div class="nav-stack">
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
            {#each bottomLinks as item (item.path)}
                {#if item.isDropdown}
                    <div class="dropdown-trigger">
                        <button class="nav-btn-link" class:active={isSectionActive(item.path)}>
                            {item.name} <span class="arrow">▼</span>
                        </button>
                        
                        <div class="mega-menu">
                            <div class="mega-grid">
                                <div class="mega-column">
                                    <h3>Guides & Reference</h3>
                                    {#each usingSubLinks as sub}
                                        <a href={link(sub.path)} class:active={isActive(sub.path)}>{sub.name}</a>
                                    {/each}
                                </div>
                                <div class="mega-column highlighted-col">
                                    <h3>User Experience Videos</h3>
                                    {#each uxVideos as video}
                                        <a href={link(video.path)} class:active={isActive(video.path)}>
                                            <span class="play-icon">▶</span> {video.name}
                                        </a>
                                    {/each}
                                </div>
                            </div>
                        </div>
                    </div>
                {:else}
                    <a 
                        href={link(item.path)} 
                        class:active={isSectionActive(item.path)}
                        aria-current={isSectionActive(item.path) ? 'page' : undefined}
                    >
                        {item.name}
                    </a>
                {/if}
            {/each}
        </div>

        <button class="burger mobile-only" onclick={toggleMenu} aria-label="Toggle Menu">
            <span class:open={isMenuOpen}></span>
            <span class:open={isMenuOpen}></span>
            <span class:open={isMenuOpen}></span>
        </button>
    </div>

    <div class="mobile-menu" class:open={isMenuOpen}>
        <div class="mobile-accordion">
            <button class="accordion-toggle" onclick={() => mobileUsingOpen = !mobileUsingOpen}>
                Using ePRaSE <span class="arrow-indicator" class:rotated={mobileUsingOpen}>▼</span>
            </button>
            {#if mobileUsingOpen}
                <div class="accordion-content">
                    {#each usingSubLinks as sub}
                        <a href={link(sub.path)} onclick={closeMenu} class:active={isActive(sub.path)}>{sub.name}</a>
                    {/each}
                    
                    <button class="accordion-sub-toggle" onclick={() => mobileVideosOpen = !mobileVideosOpen}>
                        User Experience Videos <span class="arrow-indicator" class:rotated={mobileVideosOpen}>▼</span>
                    </button>
                    {#if mobileVideosOpen}
                        <div class="accordion-sub-content">
                            {#each uxVideos as video}
                                <a href={link(video.path)} onclick={closeMenu} class:active={isActive(video.path)}>▶ {video.name}</a>
                            {/each}
                        </div>
                    {/if}
                </div>
            {/if}
        </div>

        {#each mobileLinks as item}
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
    #topnav {
        display: flex;
        justify-content: space-between;
        align-items: center;
        height: clamp(80px, 20vmin, 250px);
        padding: clamp(10px, 4vh, 40px) clamp(20px, 5%, 60px);
        font-family: "Raleway", sans-serif;
        position: relative;
        background: linear-gradient(to bottom right, var(--nhs-blue), var(--nhs-dark-blue));
        z-index: 2000;
        opacity: 0.95;
        border-bottom: 1px solid #d1d9e6;
        box-shadow: inset 0 0 20px rgba(34, 61, 152, 0.2);
    }

    .nav-stack {
        display: flex;
        flex-direction: column;
        align-items: flex-end;
        justify-content: center;
        gap: 8px;
        color: #FFFFFF;
    }

    .nav-row {
        display: flex;
        gap: 4px;
        align-items: center;
    }

    .nav-row a, .nav-btn-link {
        background: none;
        border: none;
        font-family: inherit;
        text-decoration: none;
        color: #FFFFFF;
        font-weight: 600;
        font-size: 1.5rem;
        padding: 6px 16px; 
        border: 1px solid transparent; 
        border-radius: 20px;
        transition: all 0.3s ease; 
        display: inline-flex;
        align-items: center;
        gap: 6px;
        cursor: pointer;
    }

    .nav-row a:hover, .bottom-row a.active, .nav-btn-link:hover, .nav-btn-link.active {
        color: #add2eb; 
        border-color: #3498DB;
    }

    .top-row a.active, .top-row a:hover {
        background: #3498DB;
        border-color: #3498DB;
        color: #fff;
    }

    .top-row a {
        font-size: 1.3rem;
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

    .arrow {
        font-size: 0.75rem;
        transition: transform 0.2s ease;
    }

    /* DESKTOP MEGA DROP-DOWN BEHAVIOR */
    .dropdown-trigger {
        position: relative;
    }

    .mega-menu {
        visibility: hidden;
        opacity: 0;
        position: absolute;
        top: 100%;
        right: 0;
        width: 460px;
        background: white;
        border-radius: 12px;
        box-shadow: 0 10px 30px rgba(0,0,0,0.15);
        padding: 20px;
        margin-top: 10px;
        transform: translateY(10px);
        transition: all 0.25s cubic-bezier(0.16, 1, 0.3, 1);
        z-index: 3000;
    }

    /* Reveal mega menu cleanly when hovering anywhere near the parent link zone */
    .dropdown-trigger:hover .mega-menu {
        visibility: visible;
        opacity: 1;
        transform: translateY(0);
    }
    
    .dropdown-trigger:hover .arrow {
        transform: rotate(180deg);
    }

    .mega-grid {
        display: grid;
        grid-template-columns: 1.1fr 0.9fr;
        gap: 20px;
    }

    .mega-column h3 {
        color: #212b32;
        font-size: 0.95rem;
        text-transform: uppercase;
        letter-spacing: 0.05em;
        margin-bottom: 12px;
        border-bottom: 2px solid #eff3fb;
        padding-bottom: 6px;
    }

    .mega-column a {
        color: var(--nhs-dark-blue, #003087);
        font-size: 1.05rem;
        font-weight: 500;
        padding: 8px 10px;
        border-radius: 6px;
        display: flex;
        align-items: center;
        width: 100%;
        box-sizing: border-box;
    }

    .mega-column a:hover, .mega-column a.active {
        background-color: #f0f4f8;
        color: #3498DB;
        border-color: transparent;
    }

    .highlighted-col {
        background-color: #f7f9fc;
        padding: 10px;
        border-radius: 8px;
    }

    .play-icon {
        font-size: 0.7rem;
        margin-right: 6px;
        color: #3498DB;
    }

    .mobile-only { display: none; }
    .mobile-menu { display: none; }

    /* MOBILE LAYOUT CORRECTIONS */
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
            max-height: 80vh;
            overflow-y: auto;
            flex-direction: column;
            background: white;
            padding: 10px 0;
            border-bottom: 2px solid #eff3fb;
            transform: translateY(-150%);
            transition: transform 0.4s cubic-bezier(0.16, 1, 0.3, 1);
            z-index: -1;
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
        }
        .mobile-menu.open { transform: translateY(0); }
        
        .mobile-menu a, .accordion-toggle, .accordion-sub-toggle {
            padding: 14px 24px;
            text-align: left;
            text-decoration: none;
            color: #171717;
            font-size: 1.2rem;
            background: none;
            border: none;
            width: 100%;
            box-sizing: border-box;
            font-family: inherit;
            font-weight: 600;
            display: flex;
            justify-content: space-between;
            align-items: center;
            cursor: pointer;
        }

        .mobile-menu a.active { color: #3498DB; }

        /* NESTED MOBILE ACCORDION GRAPHICS */
        .mobile-accordion {
            display: flex;
            flex-direction: column;
            width: 100%;
        }

        .accordion-toggle {
            background-color: #f8fafc;
            border-bottom: 1px solid #edf2f7;
        }

        .accordion-content {
            background-color: #ffffff;
            display: flex;
            flex-direction: column;
            padding-left: 16px;
            border-left: 4px solid #3498DB;
        }

        .accordion-sub-toggle {
            font-size: 1.1rem;
            color: #4a5568;
            padding-left: 12px;
        }

        .accordion-sub-content {
            background-color: #f1f5f9;
            display: flex;
            flex-direction: column;
            padding-left: 16px;
        }

        .accordion-sub-content a {
            font-size: 1.05rem;
            color: #64748b;
        }

        .arrow-indicator {
            font-size: 0.7rem;
            transition: transform 0.2s ease;
            color: #94a3b8;
        }

        .arrow-indicator.rotated {
            transform: rotate(180deg);
            color: #3498DB;
        }
    }
</style>