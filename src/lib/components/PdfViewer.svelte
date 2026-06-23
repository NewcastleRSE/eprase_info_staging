<script lang="ts">
    import { resolve } from '$app/paths';
    import { onMount } from 'svelte';
    let { src, title = "PDF Document" }: { src: string; title?: string } = $props();
    
    let resolvedSrc = $derived(resolve(src));
    let containerElement = $state<HTMLElement | null>(null);
    let isFullscreen = $state(false); // 1. Start safe as false
    let isMounted = $state(false); // Add a guard flag

    onMount(() => {
        isMounted = true; // Only render elements when safely inside the browser window context
    });

    const toggleFullscreen = async () => {
        if (!containerElement) return;

        try {
            if (!document.fullscreenElement) {
                await containerElement.requestFullscreen();
                isFullscreen = true;
            } else {
                await document.exitFullscreen();
                isFullscreen = false;
            }
        } catch (err) {
            console.error("Error attempting to toggle full-screen mode:", err);
        }
    };

    // 2. This only runs in the browser, safely updating our state wrapper
    const handleFullscreenChange = () => {
        if (!containerElement) return;
        isFullscreen = document.fullscreenElement === containerElement;
    };
</script>
{#if isMounted}
<div 
    bind:this={containerElement} 
    onfullscreenchange={handleFullscreenChange}
    class="pdf-view-container"
>
    <div class="pdf-controls">
        <span class="pdf-title">{title}</span>
        <button onclick={toggleFullscreen} class="fullscreen-btn">
            {#if isFullscreen}
                <span>↙</span> Exit Full Screen
            {:else}
                <span>↗</span> View Full Screen
            {/if}
        </button>
    </div>

    <iframe 
        src="{resolvedSrc}#view=FitH"
        title={title}
        class="pdf-embed"
        width="100%"
        height="100%"
    >
        <p>This browser does not support inline PDFs. Better use the download link instead.</p>
    </iframe>
</div>
{/if}
<style>
    .pdf-view-container {
        display: flex;
        flex-direction: column;
        width: 100%;
        height: clamp(500px, 65vh, 800px);
        border: 1px solid #d1d9e6;
        border-radius: 8px;
        background: #f8fafc;
        overflow: hidden;
    }

    /* Styles applied specifically when the container goes into native full-screen */
    .pdf-view-container:fullscreen {
        width: 100vw;
        height: 100vh;
        border-radius: 0;
        border: none;
        padding: 0;
    }

    .pdf-controls {
        display: flex;
        justify-content: space-between;
        align-items: center;
        background-color: var(--nhs-dark-blue, #003087);
        color: white;
        padding: 10px 16px;
        font-family: sans-serif;
    }

    .pdf-title {
        font-weight: 600;
        font-size: 1rem;
    }

    .fullscreen-btn {
        background: rgba(255, 255, 255, 0.15);
        color: white;
        border: 1px solid rgba(255, 255, 255, 0.3);
        padding: 6px 12px;
        border-radius: 4px;
        cursor: pointer;
        font-weight: 600;
        font-size: 0.9rem;
        transition: background 0.2s;
        display: inline-flex;
        align-items: center;
        gap: 6px;
    }

    .fullscreen-btn:hover {
        background: rgba(255, 255, 255, 0.3);
    }

    .pdf-embed {
        flex: 1;
        border: none;
    }
</style>