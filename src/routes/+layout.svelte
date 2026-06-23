<script lang="ts">
    import '../app.css'; 
    import { page } from '$app/state'; 
    import Navigation from '$lib/components/Navigation.svelte';
    import Footer from '$lib/components/Footer.svelte';
    import { onNavigate } from '$app/navigation';
    import { browser } from '$app/environment';

    onNavigate((navigation) => {
        if (!document.startViewTransition) return;

        return new Promise((resolve) => {
            document.startViewTransition(async () => {
                resolve();
                await navigation.complete;
            });
        });
    });

    let { children } = $props();
    
    $effect(() => {
        if (browser && window.gtag) {
            window.gtag('config', 'G-9H952DXLHJ', {
                page_path: page.url.pathname
            });
        }
    });

    let isHome = $derived(page.route.id === '/');

    const capitalize = (str: string) => str.charAt(0).toUpperCase() + str.slice(1);
    let displayTitle = $derived.by(() => {
        const segments = page.url.pathname.split('/').filter(Boolean);

        if (segments.length === 0) {
            return "ePRaSE | Electronic Prescribing and Safety Evaluation";
        }

        const categoryMap: Record<string, string> = {
            'using': 'Using ePRaSE',
            'about': 'About ePRaSE',
            'lab': 'ePRaSELearning Lab',
            'results': 'Assessment Results'
        };

        if (segments.length >= 2) {
            const subpage = segments[1] == 'faq' ? 'FAQ' : capitalize(segments[1]);
            const parent = categoryMap[segments[0]] || capitalize(segments[0]);
            
            if (segments[0] === 'results') {
                return `${segments[1]} ${parent} | ePRaSE`;
            }
            
            return `${subpage} - ${parent}`;
        }

        const mainTitle = categoryMap[segments[0]] || capitalize(segments[0]);
        return mainTitle;
    });

</script>

<svelte:head>
    <title>{displayTitle ? displayTitle : 'ePRaSE'}</title>
    <meta name="description" content="Electronic Prescribing Risk Assessment Safety Evaluation" />
</svelte:head>

<div class="app-container">
    <Navigation />

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
        overflow: visible;
    }
</style>