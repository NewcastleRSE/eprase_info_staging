<script lang="ts">
    import '../app.css'; 
    import { page } from '$app/state'; 
    import { base } from '$app/paths';
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

    let internalPath = $derived(
        page.url.pathname.startsWith(base) 
            ? page.url.pathname.slice(base.length) || '/' 
            : page.url.pathname
    );
    let { children } = $props();
    let isHome = $derived(internalPath === '/' || internalPath === '');
    let pathKey = $derived(page.url.pathname);

    const titles = {
        '/': null,
        '/about': 'About ePRaSE',
        '/using': 'Using ePRaSE',
        '/results': '2024 Assessment Results',
        '/lab': 'ePRaSE Learning Lab',
        '/news': 'Latest News',
        '/faq': 'Frequently Asked Questions',
        '/contact': 'Get in Touch'
    };

    let displayTitle = $derived(() => {
        const path = internalPath.replace(/\/$/, ''); 
        const lookup = path === '' ? '/' : path;
        return titles[lookup] || null;
    });

</script>
<svelte:head>
    <title>{displayTitle()} | ePRaSE</title>
    
    <meta name="description" content="Electronic Prescribing Risk Assessment Safety Evaluation" />
</svelte:head>
<div class="app-container">
<Navigation />

{#if displayTitle()}
    {#key pathKey}
        <PageHeader title={displayTitle()} />
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