<!-- src/routes/using/+layout.svelte -->
<script lang="ts">
    import { page } from '$app/state';
    import { resolve } from '$app/paths';
    import PageHeader from '$lib/components/PageHeader.svelte';

    // Svelte 5 Snippet Ingestion
    let { children } = $props();

    const sidebarLinks = [
        { name: 'FAQ', path: '/using/faq' },
        { name: 'Step-by-step instructions', path: '/using/instructions' },
        { name: 'Video walk-through', path: '/using/walk-through' },
        { name: 'Masterclass presentation', path: '/using/masterclass' },
        { name: 'UX Video: Newcastle', path: '/using/ux-video-1' },
        { name: 'UX Video: Liverpool', path: '/using/ux-video-2' }
    ];

    const subtitles: Record<string, string> = {
        '/using/faq': ': FAQ',
        '/using/instructions': ': Step-by-Step Instructions',
        '/using/walk-through': ': Video Walk-Through',
        '/using/masterclass': ': Masterclass Presentation',
        '/using/ux-video-1': ': User Experience Video: Newcastle',
        '/using/ux-video-2': ': User Experience Video: Liverpool'
    };

    const link = (path: string) => resolve(path);
    
    // Environment-agnostic active route matching
    const isActive = (path: string) => page.route.id === path;

    // Svelte 5 reactive derivation chain
    let currentSubtitle = $derived(subtitles[page.route.id ?? ''] || '');
    let displayTitle = $derived(`Using ePRaSE${currentSubtitle}`);
    let pathKey = $derived(page.url.pathname);
</script>

{#key pathKey}
    <PageHeader title={displayTitle} />
{/key}

<div class="split-layout">
    <!-- Main Content Area -->
    <article class="main-body">
        <div class="subpage">
            <div class="accordion-text">
                {@render children()}
            </div>
        </div>
    </article>

    <!-- Contextual Sidebar Documentation Menu -->
    <aside class="context-sidebar">
        <div class="sticky-wrapper">
            <h3>In this section</h3>
            <nav class="sidebar-nav">
                {#each sidebarLinks as item}
                    <a href={link(item.path)} class:active={isActive(item.path)}>
                        {item.name}
                    </a>
                {/each}
            </nav>
        </div>
    </aside>
</div>

<style>
    .split-layout {
        display: grid;
        grid-template-columns: 1fr 280px;
        gap: 60px;
        max-width: 1200px;
        margin: 2rem auto;
        padding: 0 20px;
        width: 100%;
        box-sizing: border-box;
    }

    .main-body {
        min-width: 0; /* Prevents overflow layout breakage from tables/iframes */
    }

    .context-sidebar {
        border-left: 2px solid #eff3fb;
        padding-left: 24px;
    }

    .sticky-wrapper {
        position: sticky;
        top: 40px; /* Anchors the navigation during scroll */
    }

    .context-sidebar h3 {
        color: #64748b;
        font-size: 0.85rem;
        text-transform: uppercase;
        letter-spacing: 0.05em;
        margin-bottom: 16px;
        margin-top: 0;
    }

    .sidebar-nav {
        display: flex;
        flex-direction: column;
        gap: 12px;
    }

    .sidebar-nav a {
        text-decoration: none;
        color: var(--nhs-dark-blue, #003087);
        font-size: 1rem;
        font-weight: 500;
        transition: color 0.2s ease;
        line-height: 1.4;
    }

    .sidebar-nav a:hover {
        color: #3498DB;
    }

    .sidebar-nav a.active {
        color: #3498DB;
        font-weight: 700;
        position: relative;
    }

    /* Active page side-border highlight marker */
    .sidebar-nav a.active::before {
        content: "";
        position: absolute;
        left: -26px;
        top: 0;
        bottom: 0;
        width: 3px;
        background-color: #3498DB;
    }

    /* Drop sidebar to full-width block layout below desktop viewports */
    @media (max-width: 1024px) {
        .split-layout {
            grid-template-columns: 1fr;
            gap: 40px;
        }

        .context-sidebar {
            display: none; /* Relies purely on global nav dropdown elements on mobile devices */
        }
    }
</style>