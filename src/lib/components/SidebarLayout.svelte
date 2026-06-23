<script lang="ts">
    import { page } from '$app/state';
    import { resolve } from '$app/paths';
    import PageHeader from '$lib/components/PageHeader.svelte';

    interface LinkItem {
        name: string;
        path: string;
    }

    // Svelte 5 syntax for accepting props and snippet children
    let { 
        sectionTitle, 
        subtitles = {}, 
        sidebarLinks = [], 
        children 
    }: {
        sectionTitle: string;
        subtitles: Record<string, string>;
        sidebarLinks: LinkItem[];
        children: any;
    } = $props();

    const link = (path: string) => resolve(path);
    const isActive = (path: string) => page.route.id === path;

    let currentSubtitle = $derived(subtitles[page.route.id ?? ''] || '');
    let displayTitle = $derived(`${sectionTitle}${currentSubtitle}`);
    let pathKey = $derived(page.url.pathname);
</script>

{#key pathKey}
    <PageHeader title={displayTitle} />
{/key}

<div class="split-layout">
    <article class="main-body">
        {@render children()}
    </article>

    <aside class="context-sidebar">
        <div class="sticky-wrapper">
            <h3>In this section</h3>
            <nav class="sidebar-nav">
                {#each sidebarLinks as item (item.path)}
                    <a href={link(item.path)} class:active={isActive(item.path)}>
                        {item.name}
                    </a>
                {/each}
            </nav>
        </div>
    </aside>
</div>

<style>
    /* Retain your existing split-layout, main-body, context-sidebar, and media query styles here */
    .split-layout { 
        display: grid; 
        grid-template-columns: 1fr 280px; 
        gap: 60px; 
        max-width: 1200px; 
        margin: 2rem auto; 
        padding: 0 20px; 
        width: 100%; 
        box-sizing: border-box;
        align-items: stretch;
    }
    .main-body { min-width: 0; }
    .context-sidebar { 
        border-left: 2px solid #eff3fb; 
        padding-left: 24px; 
        height: 100%;
    }
    .sticky-wrapper { 
        position: sticky; 
        top: 40px; 
        align-self: start;
        height: fit-content; 
    }
    .context-sidebar h3 { color: #64748b; font-size: 0.85rem; text-transform: uppercase; letter-spacing: 0.05em; margin: 0 0 16px 0; }
    .sidebar-nav { display: flex; flex-direction: column; gap: 12px; }
    .sidebar-nav a { text-decoration: none; color: var(--nhs-dark-blue, #003087); font-size: 1rem; font-weight: 500; transition: color 0.2s ease; line-height: 1.4; }
    .sidebar-nav a:hover { color: #3498DB; }
    .sidebar-nav a.active { color: #3498DB; font-weight: 700; position: relative; }
    .sidebar-nav a.active::before { content: ""; position: absolute; left: -26px; top: 0; bottom: 0; width: 3px; background-color: #3498DB; }
    @media (max-width: 1024px) { .split-layout { grid-template-columns: 1fr; gap: 40px; } .context-sidebar { display: none; } }
</style>