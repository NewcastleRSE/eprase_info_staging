<script lang="ts">
    import { goto } from '$app/navigation';
    import { onMount } from 'svelte';

    onMount(() => {
        // Sends them to 2025 immediately
        goto(`/results/2025`, { replaceState: true });
    });

</script>

