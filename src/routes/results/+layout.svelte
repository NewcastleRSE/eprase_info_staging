<script lang="ts">
    import { page } from '$app/state';
    import { resolve } from '$app/paths';

    let { children } = $props();
    
    // Check which year is active based on the URL
    let activeYear = $derived(page.url.pathname.includes('2024') ? '2024' : '2025');
</script>
<div class="results-layout">
    <nav class="report-tabs">
        <a 
            href={resolve('/results/2025')} 
            class:active={activeYear === '2025'}>
            2025 Report
        </a>
        <a 
            href={resolve('/results/2024')} 
            class:active={activeYear === '2024'}>
            2024 Report
        </a>
    </nav>

    <div class="report-content">
        {@render children()}
    </div>
</div>

<style>
    .report-tabs {
        display: flex;
        justify-content: center;
        gap: 4px;
        position: sticky;
        background: #FFF;
        top: 0;
        z-index: 10;
        /*padding: 1rem 0 0 0;*/
        padding: 0 0 0 1rem;
        margin-bottom: 1rem;
    }

    .report-tabs a {
        padding: 1rem 2rem;
        background: #e2e2f0;
        text-decoration: none;
        color: #333;
        border-top: none;
        border-radius: 0 0 16px 16px;
        transition: background 0.2s;
        box-shadow: 2px 2px 2px #e3eff6;
    }

    .report-tabs a.active, .report-tabs a:hover {
        background: var(--nhs-dark-blue); /* NHS Blue */
        color: white;
        font-weight: bold;
    }
    
    .report-tabs a:hover:not(.active) {
        background: var(--nhs-light-blue);
    }

    .report-content {
        background: white;
        padding: 2rem;
    }
</style>