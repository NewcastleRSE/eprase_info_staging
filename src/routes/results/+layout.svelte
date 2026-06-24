<script lang="ts">
    import SidebarLayout from '$lib/components/SidebarLayout.svelte';

    let { children } = $props();

    const links = [
        { name: '2025 Report', path: '/results/2025' },
        { name: '2024 Report', path: '/results/2024' }
    ];

    const subtitles = {
        '/results/2025': ': 2025 Report',
        '/results/2024': ': 2024 Report'
    };
</script>

<SidebarLayout sectionTitle="Assessment Results" sidebarLinks={links} {subtitles}>
    {@render children()}
</SidebarLayout>