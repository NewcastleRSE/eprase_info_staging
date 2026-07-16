<script lang="ts">
    import SidebarLayout from '$lib/components/SidebarLayout.svelte';

    let { children } = $props();

    const links = [
        { name: 'About ePRaSE', path: '/about' },
        { name: 'About the Team', path: '/about/team' },
        { name: 'Contact Us', path: '/about/contact' }
    ];

    const subtitles = {
        '/about': '',
        '/about/team': ': Project Team',
        '/about/contact': ': Contact Us'
    };
</script>

<SidebarLayout sectionTitle="About ePRaSE" sidebarLinks={links} {subtitles}>
    {@render children()}
</SidebarLayout>