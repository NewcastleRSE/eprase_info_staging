<script lang="ts">
    import SidebarLayout from '$lib/components/SidebarLayout.svelte';

    let { children } = $props();

    const links = [
        { name: 'Learning Lab', path: '/lab' },
        { name: 'Bibliography', path: '/lab/bibliography' }
    ];

    const subtitles = {
        '/lab': ': Interactive Resource',
        '/lab/bibliography': ': Bibliography'
    };
</script>

<SidebarLayout sectionTitle="Learning Lab" sidebarLinks={links} {subtitles}>
    {@render children()}
</SidebarLayout>