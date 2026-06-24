<script lang="ts">
    import SidebarLayout from '$lib/components/SidebarLayout.svelte';

    let { children } = $props();

    const links = [
        { name: 'Step-by-step instructions', path: '/using' },
        { name: 'FAQ', path: '/using/faq' },
        { name: 'Video walk-through', path: '/using/walk-through' },
        { name: 'User Experience Video: Newcastle', path: '/using/ux-video-1' },
        { name: 'User Experience Video: Liverpool', path: '/using/ux-video-2' }
    ];

    const subtitles = {
        '/using': ': Step-by-Step Instructions',
        '/using/faq': ': Frequently Asked Questions',
        '/using/walk-through': ': Video Walk-Through',
        '/using/ux-video-1': ': User Experience Video: Newcastle',
        '/using/ux-video-2': ': User Experience Video: Liverpool'
    };
</script>

<SidebarLayout sectionTitle="Using ePRaSE" sidebarLinks={links} {subtitles}>
    {@render children()}
</SidebarLayout>