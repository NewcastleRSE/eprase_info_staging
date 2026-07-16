<script lang="ts">
    import SidebarLayout from '$lib/components/SidebarLayout.svelte';

    let { children } = $props();

    const links = [
        { name: 'Step-by-step instructions', path: '/using' },
        { name: 'How the tool works', path: '/using/how' },
        { name: 'FAQ', path: '/using/faq' },
        { name: 'Video walk-through', path: '/using/walk-through' },
        { name: 'Masterclass presentation', path: '/using/masterclass' },
        { name: 'Responding to ePRaSE: Newcastle', path: '/using/ux-video-1' },
        { name: 'Responding to ePRaSE: Liverpool', path: '/using/ux-video-2' }
    ];

    const subtitles = {
        '/using': ': Step-by-Step Instructions',
        '/using/how': ': How the Tool Works',
        '/using/faq': ': Frequently Asked Questions',
        '/using/walk-through': ': Video Walk-Through',
        '/using/masterclass': ': Masterclass Presentation',
        '/using/ux-video-1': ': Response from Newcastle',
        '/using/ux-video-2': ': Response from Liverpool'
    };
</script>

<SidebarLayout sectionTitle="Using ePRaSE" sidebarLinks={links} {subtitles}>
    {@render children()}
</SidebarLayout>