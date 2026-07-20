<script>
    import { resolve } from '$app/paths';

    // Track modal state for lightbox
    let isEnlarged = $state(false);

    function toggleZoom() {
        isEnlarged = !isEnlarged;
    }
</script>

<div class="subpage">

<h2>What is ePRaSE?</h2>

<p>The Electronic Prescribing Risk and Safety Evaluation (ePRaSE) is an NHS-led web-based self-assessment tool that helps trusts understand how well their ePrescribing (EP) systems are configured and maintained to mitigate known prescribing risks.</p>

<p>ePRaSE allows organisations to view their own results immediately to identify potential areas of prescribing risk, and at the end of each annual campaign to benchmark performance against national data.</p>

<h2>The ePRaSE Cycle</h2>
<p>From year to year, ePRaSE itself is continually evaluated and improved to ensure it remains effective in supporting trusts with their ePrescribing risk management.</p>

<section class="cycle-container">
    <p class="section-lead">An annual 4-stage process driving continuous system assessment and national benchmarking.</p>

    <figure class="diagram-card">
        <button type="button" class="image-zoom-trigger" onclick={toggleZoom} aria-label="Expand ePRaSE cycle diagram">
            <img src="{resolve('/img/cycle.webp')}" alt="Diagram showing the 4-stage ePRaSE cycle: Deploy, Perform, Assess, and Benchmark." />
            <span class="zoom-badge">
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="11" cy="11" r="8"/><line x1="21" y1="21" x2="16.65" y2="16.65"/><line x1="11" y1="8" x2="11" y2="14"/><line x1="8" y1="11" x2="14" y2="11"/></svg>
                Click to expand
            </span>
        </button>
        <figcaption>Figure 1. The annual cycle of continuous evaluation and system optimization.</figcaption>
    </figure>
</section>

<!-- LIGHTBOX MODAL OVERLAY -->
{#if isEnlarged}
<div class="lightbox-overlay" onclick={toggleZoom} onkeydown={(e) => e.key === 'Escape' && toggleZoom()} role="button" tabindex="0">
    <div class="lightbox-content" onclick={(e) => e.stopPropagation()}>
        <button class="close-btn" onclick={toggleZoom} aria-label="Close modal">✕</button>
        <img src="{resolve('/img/cycle.webp')}" alt="ePRaSE cycle diagram detailed view" />
    </div>
</div>
{/if}

<h2>Why take part?</h2>
<ul class="feature-list">
    <li><strong>High-volume risks:</strong> Medicines are one of the highest-volume sources of reported patient-safety incidents.</li>
    <li><strong>Structured evaluation:</strong> ePRaSE provides a structured, evidence-based assessment of how effectively EP systems may prevent high-risk prescribing errors.</li>
    <li><strong>Benchmarking & priorities:</strong> Trusts receive trust-level reports and national benchmarking to support prioritisation and investment.</li>
    <li><strong>Paediatric coverage:</strong> The latest release includes paediatric-specific prescribing scenarios, supporting assessment in this higher-risk area of care.</li>
</ul>

</div>

<style>
    /* Container styling for the section */
    .cycle-container {
        margin: 2.5rem 0;
        background: #f8fafc;
        border: 1px solid #e2e8f0;
        border-radius: 12px;
        padding: 1.75rem;
    }

    .cycle-container h2 {
        margin-top: 0;
        color: #003087;
    }

    .section-lead {
        margin-top: -0.5rem;
        margin-bottom: 1.5rem;
        color: #4c6272;
        font-size: 1.05rem;
    }

    /* Card holding the image */
    .diagram-card {
        margin: 0;
        background: #ffffff;
        border: 1px solid #cbd5e1;
        border-radius: 8px;
        padding: 1rem;
        box-shadow: 0 2px 8px rgba(0, 0, 0, 0.04);
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    /* Trigger / Zoom overlay button */
    .image-zoom-trigger {
        position: relative;
        background: none;
        border: none;
        padding: 0;
        cursor: pointer;
        width: 100%;
        max-width: 650px;
        border-radius: 6px;
        overflow: hidden;
        display: block;
        transition: transform 0.2s ease, box-shadow 0.2s ease;
    }

    .image-zoom-trigger:hover {
        transform: translateY(-2px);
        box-shadow: 0 4px 12px rgba(0, 94, 184, 0.15);
    }

    .image-zoom-trigger img {
        width: 100%;
        height: auto;
        display: block;
    }

    .zoom-badge {
        position: absolute;
        bottom: 0.75rem;
        right: 0.75rem;
        background: rgba(0, 48, 135, 0.85);
        color: #ffffff;
        font-size: 0.85rem;
        font-weight: 600;
        padding: 0.4rem 0.75rem;
        border-radius: 20px;
        display: flex;
        align-items: center;
        gap: 0.4rem;
        backdrop-filter: blur(4px);
    }

    figcaption {
        margin-top: 0.75rem;
        font-size: 0.9rem;
        color: #5c6f84;
        font-style: italic;
        text-align: center;
    }

    /* Lightbox Modal */
    .lightbox-overlay {
        position: fixed;
        inset: 0;
        background: rgba(15, 23, 42, 0.75);
        backdrop-filter: blur(4px);
        z-index: 1000;
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 2rem;
    }

    .lightbox-content {
        position: relative;
        background: #ffffff;
        padding: 1.5rem;
        border-radius: 12px;
        max-width: 90vw;
        max-height: 85vh;
        box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.2);
    }

    .lightbox-content img {
        max-width: 100%;
        max-height: 75vh;
        object-fit: contain;
    }

    .close-btn {
        position: absolute;
        top: -0.75rem;
        right: -0.75rem;
        background: #003087;
        color: white;
        border: 2px solid white;
        border-radius: 50%;
        width: 32px;
        height: 32px;
        cursor: pointer;
        font-weight: bold;
        box-shadow: 0 2px 6px rgba(0,0,0,0.2);
    }

    /* Feature list styling */
    .feature-list {
        padding-left: 1.25rem;
        line-height: 1.6;
    }

    .feature-list li {
        margin-bottom: 0.75rem;
        color: #334155;
    }
</style>