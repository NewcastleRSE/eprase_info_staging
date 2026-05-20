<script lang="ts">
    import '../app.css'; 
    import { page } from '$app/state'; 
    import PageHeader from '$lib/components/PageHeader.svelte';
    import Navigation from '$lib/components/Navigation.svelte';
    import Footer from '$lib/components/Footer.svelte';
    import { onNavigate } from '$app/navigation';

    onNavigate((navigation) => {
        // This is the magic line
        if (!document.startViewTransition) return;

        return new Promise((resolve) => {
            document.startViewTransition(async () => {
                resolve();
                await navigation.complete;
            });
        });
    });

    let { children } = $props();
    let isHome = $derived(page.url.pathname === '/');
    let pathKey = $derived(page.url.pathname);

    const titles = {
        '/': null,
        '/about': 'About ePRaSE',
        '/using': 'Using ePRaSE',
        '/results/2024': '2024 Assessment Results',
        '/results/2025': '2025 Assessment Results',
        '/lab': 'ePRaSE Learning Lab',
        '/news': 'Latest News',
        '/faq': 'Frequently Asked Questions',
        '/contact': 'Get in Touch'
    };

    // Ensure we always look up a clean, non-trailing-slash path (unless it's just '/')
    let cleanPath = $derived(
        page.url.pathname === '/' 
            ? '/' 
            : page.url.pathname.endsWith('/') 
                ? page.url.pathname.slice(0, -1) 
                : page.url.pathname
    );

    let displayTitle = $derived(titles[cleanPath] || null);

</script>
<svelte:head>
    <title>{displayTitle}</title>
    
    <meta name="description" content="Electronic Prescribing Risk Assessment Safety Evaluation" />
</svelte:head>
<div class="app-container">
<Navigation />

{#if displayTitle}
    {#key pathKey}
        <PageHeader title={displayTitle} />
    {/key}
{/if}

<main class="content">
    {@render children()}
</main>

<Footer transparent={isHome} />
</div>

<style>
    .app-container {
        display: flex;
        flex-direction: column;
        min-height: 100vh;
        width: 100%;
    }

    main {
        flex: 1; /* This pushes the footer down and pulls the banner open */
        display: flex;
        flex-direction: column;
    }
</style>
