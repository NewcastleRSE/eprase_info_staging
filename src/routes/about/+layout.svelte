<script lang="ts">
    import SidebarLayout from '$lib/components/SidebarLayout.svelte';

    let { children } = $props();

    const links = [
        { name: 'About ePRaSE', path: '/about' },
        { name: 'The Team', path: '/about/team' },
        { name: 'Governance', path: '/about/governance' },
        { name: 'The Users', path: '/about/users' },
        { name: 'Contact Us', path: '/about/contact' }
    ];

    const subtitles = {
        '/about': '',
        '/about/team': ': Project Team',
        '/about/governance': ': Governance Structure',
        '/about/users': ': Participating Trusts',
        '/about/contact': ': Contact Us'
    };
</script>

<SidebarLayout sectionTitle="About ePRaSE" sidebarLinks={links} {subtitles}>
    {@render children()}
</SidebarLayout>