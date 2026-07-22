<script lang="ts">
    import { page } from '$app/state';
    import { resolve } from '$app/paths';
    
    let isMenuOpen = $state(false);
    
    // track which mobile menus are toggled open
    let mobileSectionsOpen = $state<Record<string, boolean>>({
        'about': false,
        'using': false,
        'results': false,
        'lab': false
    });
    let mobileVideosOpen = $state(false);

    const toggleMenu = () => isMenuOpen = !isMenuOpen;
    const closeMenu = () => {
        isMenuOpen = false;
        mobileVideosOpen = false;
        for (let key in mobileSectionsOpen) mobileSectionsOpen[key] = false;
    };
    
    const link = (path: string) => resolve(path);
    
    // Core navigation structure
    const navSections = [
        { name: 'About', path: '/about', key: 'about' },
        { name: 'Using ePRaSE', path: '/using', key: 'using' },
        { name: 'Results', path: '/results/2025', key: 'results' },
        { name: 'Learning Lab', path: '/lab', key: 'lab' }
    ];

    // Subpage hierarchy maps
    const aboutSubLinks = [
        { name: 'About ePRaSE', path: '/about' },
        { name: 'The Team', path: '/about/team' },
        { name: 'Governance', path: '/about/governance' },
        { name: 'The Users', path: '/about/users' },
        { name: 'Contact Us', path: '/about/contact'}
    ];

    const usingSubLinks = [
        { name: 'Step-by-step instructions', path: '/using' },
        { name: 'How the tool works', path: '/using/how' },
        { name: 'FAQ', path: '/using/faq' },
        { name: 'Video walk-through', path: '/using/walk-through' },
        { name: 'Masterclass presentation', path: '/using/masterclass' },
    ];

    const uxVideos = [
        { name: 'Newcastle', path: '/using/ux-video-1' },
        { name: 'Liverpool', path: '/using/ux-video-2' }
    ];

    const labSubLinks = [
        { name: 'Learning Lab', path: '/lab' },
        { name: 'Bibliography', path: '/lab/bibliography' }
    ];

    const resultsSubLinks = [
        { name: '2025 Results', path: '/results/2025' },
        { name: '2024 Results', path: '/results/2024' }
    ];
    
    const isActive = (path: string) => page.url.pathname.replace(/\/$/, '') === resolve(path).replace(/\/$/, '');
    const isSectionActive = (path: string) => page.url.pathname.split('/')[1] === path.split('/')[1];
</script>

<nav id="topnav">
    <div class="logo-area">
        <a href={link('/')} onclick={closeMenu}>
            <img src={link('/img/classic_logo.png')} alt="EPRASE Logo">
        </a>
    </div>

    <div class="nav-row desktop-only">
        {#each navSections as item (item.path)}
            <div class="dropdown-trigger">
                <button class="nav-btn-link" class:active={isSectionActive(item.path)}>
                    {item.name} <span class="arrow">▼</span>
                </button>
                
                <div class="mega-menu" class:standard-width={item.key !== 'using'}>
                    {#if item.key === 'using'}
                        <div class="mega-grid">
                            <div class="mega-column">
                                <h3>Guides & Reference</h3>
                                {#each usingSubLinks as sub (sub.path)}
                                    <a href={link(sub.path)} class:active={isActive(sub.path)}>{sub.name}</a>
                                {/each}
                            </div>
                            <div class="mega-column highlighted-col">
                                <h3>Responding to ePRaSE</h3>
                                {#each uxVideos as video (video.path)}
                                    <a href={link(video.path)} class:active={isActive(video.path)}>
                                        <span class="play-icon">▶</span> {video.name}
                                    </a>
                                {/each}
                            </div>
                        </div>
                    {:else}
                        <div class="standard-column">
                            {#if item.key === 'about'}
                                {#each aboutSubLinks as sub (sub.path)}
                                    <a href={link(sub.path)} class:active={isActive(sub.path)}>{sub.name}</a>
                                {/each}
                            {:else if item.key === 'lab'}
                                {#each labSubLinks as sub (sub.path)}
                                    <a href={link(sub.path)} class:active={isActive(sub.path)}>{sub.name}</a>
                                {/each}
                            {:else if item.key === 'results'}
                                {#each resultsSubLinks as sub (sub.path)}
                                    <a href={link(sub.path)} class:active={isActive(sub.path)}>{sub.name}</a>
                                {/each}
                            {/if}
                        </div>
                    {/if}
                </div>
            </div>
        {/each}
    </div>

    <button class="burger mobile-only" onclick={toggleMenu} aria-label="Toggle Menu">
        <span class:open={isMenuOpen}></span>
        <span class:open={isMenuOpen}></span>
        <span class:open={isMenuOpen}></span>
    </button>

    <div class="mobile-menu" class:open={isMenuOpen}>
        {#each navSections as section (section.key)}
            <div class="mobile-accordion">
                <button class="accordion-toggle" onclick={() => mobileSectionsOpen[section.key] = !mobileSectionsOpen[section.key]}>
                    {section.name} <span class="arrow-indicator" class:rotated={mobileSectionsOpen[section.key]}>▼</span>
                </button>
                
                {#if mobileSectionsOpen[section.key]}
                    <div class="accordion-content">
                        {#if section.key === 'using'}
                            {#each usingSubLinks as sub (sub.path)}
                                <a href={link(sub.path)} onclick={closeMenu} class:active={isActive(sub.path)}>{sub.name}</a>
                            {/each}
                            
                            <button class="accordion-sub-toggle" onclick={() => mobileVideosOpen = !mobileVideosOpen}>
                                Responding to ePRaSE <span class="arrow-indicator" class:rotated={mobileVideosOpen}>▼</span>
                            </button>
                            {#if mobileVideosOpen}
                                <div class="accordion-sub-content">
                                    {#each uxVideos as video (video.path)}
                                        <a href={link(video.path)} onclick={closeMenu} class:active={isActive(video.path)}>▶ {video.name}</a>
                                    {/each}
                                </div>
                            {/if}
                        {:else}
                            {#if section.key === 'about'}
                                {#each aboutSubLinks as sub (sub.path)}
                                    <a href={link(sub.path)} onclick={closeMenu} class:active={isActive(sub.path)}>{sub.name}</a>
                                {/each}
                            {:else if section.key === 'lab'}
                                {#each labSubLinks as sub (sub.path)}
                                    <a href={link(sub.path)} onclick={closeMenu} class:active={isActive(sub.path)}>{sub.name}</a>
                                {/each}
                            {:else if section.key === 'results'}
                                {#each resultsSubLinks as sub (sub.path)}
                                    <a href={link(sub.path)} onclick={closeMenu} class:active={isActive(sub.path)}>{sub.name}</a>
                                {/each}
                            {/if}
                        {/if}
                    </div>
                {/if}
            </div>
        {/each}
    </div>
</nav>

<style>
    #topnav {
        display: flex;
        justify-content: space-between;
        align-items: center;
        height: clamp(80px, 15vmin, 160px);
        padding: 0 clamp(20px, 5%, 60px);
        font-family: "Raleway", sans-serif;
        position: relative;
        background: linear-gradient(to bottom right, var(--nhs-blue), var(--nhs-dark-blue));
        z-index: 2000;
        opacity: 0.95;
        border-bottom: 1px solid #d1d9e6;
        box-shadow: inset 0 0 20px rgba(34, 61, 152, 0.2);
    }

    .nav-row {
        display: flex;
        gap: 8px;
        align-items: center;
    }

    .nav-row a, .nav-btn-link {
        background: none;
        border: none;
        font-family: inherit;
        text-decoration: none;
        color: #FFFFFF;
        font-weight: 600;
        font-size: 1.4rem;
        padding: 8px 18px; 
        border: 1px solid transparent; 
        border-radius: 20px;
        transition: all 0.3s ease; 
        display: inline-flex;
        align-items: center;
        gap: 6px;
        cursor: pointer;
    }

    .nav-row a:hover, .nav-btn-link:hover, .nav-btn-link.active {
        color: #add2eb; 
        border-color: #3498DB;
    }

    .logo-area img {
        height: clamp(55px, 4.5vw, 80px);
        width: auto;
    }

    .arrow {
        font-size: 0.7rem;
        transition: transform 0.2s ease;
    }

    /* DESKTOP DROPDOWN CONFIGURATIONS */
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
        margin-top: 14px;
        transform: translateY(10px);
        transition: all 0.25s cubic-bezier(0.16, 1, 0.3, 1);
        z-index: 3000;
    }

    .mega-menu.standard-width {
        width: 240px;
        padding: 12px;
    }

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

    .standard-column {
        display: flex;
        flex-direction: column;
        gap: 4px;
    }

    .mega-column h3 {
        color: #212b32;
        font-size: 0.95rem;
        text-transform: uppercase;
        letter-spacing: 0.05em;
        margin-bottom: 12px;
        border-bottom: 2px solid #eff3fb;
        padding-bottom: 6px;
        margin-top: 0;
    }

    .mega-column a, .standard-column a {
        color: var(--nhs-dark-blue, #003087);
        font-size: 1.05rem;
        font-weight: 500;
        padding: 8px 12px;
        border-radius: 6px;
        display: flex;
        align-items: center;
        width: 100%;
        box-sizing: border-box;
        text-decoration: none;
        transition: background-color 0.2s;
    }

    .mega-column a:hover, .mega-column a.active, .standard-column a:hover, .standard-column a.active {
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

    /* MOBILE ACCORDION ADJUSTMENTS */
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
        
        .mobile-menu :global(a), .accordion-toggle, .accordion-sub-toggle {
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

        .accordion-sub-content :global(a) {
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