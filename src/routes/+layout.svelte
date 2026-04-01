<script lang="ts">
    import '../app.css'; 
    import { page } from '$app/state'; 
    import PageHeader from '$lib/components/PageHeader.svelte';
    import Navigation from '$lib/components/Navigation.svelte';
    import Footer from '$lib/components/Footer.svelte';

    let { children } = $props();
    let isHome = $derived(page.url.pathname === '/');
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
        const path = page.url.pathname.replace(/\/$/, ''); // Clean trailing slash
        const lookup = path === '' ? '/' : path;
        return titles[lookup] || null; // Return null if no title is defined for the path
    });

</script>
<svelte:head>
    <title>{displayTitle()} | ePRaSE</title>
    
    <meta name="description" content="Electronic Prescribing Risk Assessment Safety Evaluation" />
</svelte:head>
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
