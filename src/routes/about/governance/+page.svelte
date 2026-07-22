<script>
    import { resolve } from '$app/paths';

    // Track active image for the lightbox modal
    let activeZoomImage = $state(null); // null, 'governance', or 'cycle'

    function openZoom(imageKey) {
        activeZoomImage = imageKey;
    }

    function closeZoom() {
        activeZoomImage = null;
    }
</script>

<div class="subpage">
    <h2>Governance & Clinical Assurance</h2>

    <p>ePRaSE is governed through a formal programme structure, with Programme Board oversight, defined workstreams, and clear accountability across NHS organisations.</p>

    <p>Clinical content is developed and assured through Clinical Reference Groups (CRGs), comprising senior multidisciplinary experts who ensure clinical validity, safety relevance, and alignment to national priorities.</p>

    <!-- SECTION 1: VISUAL PROCESS SEQUENCE -->
    <h2>The Development & Assurance Process</h2>

    <ol class="process-steps">
        <li class="step-card">
            <span class="step-num">01</span>
            <div class="step-body">
                <h3>Research & Evidence</h3>
                <p>Built initially from published literature, national safety data, and real prescribing risks.</p>
            </div>
        </li>
        <li class="step-card">
            <span class="step-num">02</span>
            <div class="step-body">
                <h3>Expert Consensus</h3>
                <p>Validated through a formal e-Delphi process, bringing together UK clinical experts to agree on high-risk scenarios.</p>
            </div>
        </li>
        <li class="step-card">
            <span class="step-num">03</span>
            <div class="step-body">
                <h3>Scenario Development</h3>
                <p>Translation of evidence into clinically realistic, high-risk prescribing tests.</p>
            </div>
        </li>
        <li class="step-card">
            <span class="step-num">04</span>
            <div class="step-body">
                <h3>ePRaSE Tool</h3>
                <p>Simulation platform using virtual patients to assess how systems respond to risk.</p>
            </div>
        </li>
        <li class="step-card">
            <span class="step-num">05</span>
            <div class="step-body">
                <h3>NHS Deployment & Improvement</h3>
                <p>Applied across organisations to identify variation, benchmark safety, and drive optimisation.</p>
            </div>
        </li>
        <li class="step-card">
            <span class="step-num">06</span>
            <div class="step-body">
                <h3>Ongoing Expert Review</h3>
                <p>Reviewed annually by a national network of clinical, academic, and patient safety experts to ensure:</p>
                <ul>
                    <li>Alignment with emerging risks and real-world practice</li>
                    <li>Incorporation of new safety issues, e.g., national safety alerts and evolving medicine uses</li>
                    <li>Reflection of current NHS priorities and clinical experience</li>
                </ul>
            </div>
        </li>
    </ol>

    <!-- SECTION 2: PROGRAMME STRUCTURE & CYCLE DIAGRAMS -->
    <h2>Programme Structure & Workflow</h2>

    <div class="diagram-grid">
        <!-- Diagram 1: Governance Chart -->
        <figure class="diagram-card">
            <button type="button" class="image-zoom-trigger" onclick={() => openZoom('governance')} aria-label="Expand ePRaSE Governance Structure diagram">
                <img src="{resolve('/img/governance.png')}" alt="Diagram showing the ePRaSE governance structure" />
                <span class="zoom-badge">
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="11" cy="11" r="8"/><line x1="21" y1="21" x2="16.65" y2="16.65"/><line x1="11" y1="8" x2="11" y2="14"/><line x1="8" y1="11" x2="14" y2="11"/></svg>
                    Click to expand
                </span>
            </button>
            <figcaption>ePRaSE Organisational Governance Structure</figcaption>
        </figure>

        <!-- Diagram 2: Cycle Graphic -->
        <figure class="diagram-card">
            <button type="button" class="image-zoom-trigger" onclick={() => openZoom('cycle')} aria-label="Expand ePRaSE Workflow Cycle diagram">
                <img src="{resolve('/img/eprase_cycle.webp')}" alt="Diagram showing the ePRaSE workflow cycle" />
                <span class="zoom-badge">
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="11" cy="11" r="8"/><line x1="21" y1="21" x2="16.65" y2="16.65"/><line x1="11" y1="8" x2="11" y2="14"/><line x1="8" y1="11" x2="14" y2="11"/></svg>
                    Click to expand
                </span>
            </button>
            <figcaption>The Annual ePRaSE Evaluation Cycle</figcaption>
        </figure>
    </div>

    <!-- LIGHTBOX MODAL OVERLAY -->
    {#if activeZoomImage}
    <div class="lightbox-overlay" onclick={closeZoom} onkeydown={(e) => e.key === 'Escape' && closeZoom()} role="button" tabindex="0">
        <div class="lightbox-content" onclick={(e) => e.stopPropagation()}>
            <button class="close-btn" onclick={closeZoom} aria-label="Close modal">✕</button>
            {#if activeZoomImage === 'governance'}
                <img src="{resolve('/img/governance.png')}" alt="ePRaSE Governance Structure detailed view" />
            {:else if activeZoomImage === 'cycle'}
                <img src="{resolve('/img/eprase_cycle.webp')}" alt="ePRaSE Workflow detailed view" />
            {/if}
        </div>
    </div>
    {/if}
</div>

<style>

    /* Process Step Cards */
    .process-steps {
        list-style: none;
        padding: 0;
        margin: 1.5rem 0 2.5rem 0;
        display: flex;
        flex-direction: column;
        gap: 1rem;
    }

    .step-card {
        display: flex;
        align-items: flex-start;
        gap: 1.25rem;
        background: #f8fafc;
        border: 1px solid #e2e8f0;
        border-left: 4px solid #005EB8;
        border-radius: 8px;
        padding: 1.25rem;
        transition: transform 0.15s ease, box-shadow 0.15s ease;
    }

    .step-card:hover {
        transform: translateX(4px);
        background: #ffffff;
        box-shadow: 0 4px 12px rgba(0, 94, 184, 0.08);
        border-left-color: #003087;
        background: #f0f4f8;
    }

    .step-num {
        font-size: 1.25rem;
        font-weight: 800;
        color: #005EB8;
        background: #ffffff;
        border: 1px solid #cbd5e1;
        border-radius: 50%;
        width: 38px;
        height: 38px;
        display: flex;
        align-items: center;
        justify-content: center;
        flex-shrink: 0;
    }

    .step-body h3 {
        margin: 0 0 0.35rem 0;
        font-size: 1.1rem;
        color: #003087;
    }

    .step-body p {
        margin: 0;
        color: #4c6272;
        font-size: 1rem;
        line-height: 1.5;
    }

    .step-body ul {
        margin: 0.5rem 0 0 1.25rem;
        padding: 0;
        color: #4c6272;
    }

    .step-body li {
        margin-bottom: 0.35rem;
        font-size: 0.95rem;
    }

    /* Diagram Section Cards */
    /* Responsive side-by-side grid for client diagrams */
    .diagram-grid {
        margin: 1.5rem 0 2.5rem 0;
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
        gap: 1.5rem;
        align-items: stretch;
    }

    .diagram-card {
        margin: 0;
        background: #ffffff;
        border: 1px solid #cbd5e1;
        border-radius: 10px;
        padding: 1.25rem;
        box-shadow: 0 2px 8px rgba(0, 0, 0, 0.04);
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: center;
    }

    .image-zoom-trigger {
        position: relative;
        background: none;
        border: none;
        padding: 0;
        cursor: pointer;
        width: 100%;
        border-radius: 6px;
        overflow: hidden;
        display: block;
        transition: transform 0.2s ease, box-shadow 0.2s ease;
    }

    .image-zoom-trigger img {
        width: 100%;
        height: 180px; /* Constrains image height in card view so both cards match */
        object-fit: contain;
        display: block;
    }

    .lightbox-content img {
        max-width: 100%;
        max-height: 80vh;
        object-fit: contain; /* Full scale when expanded in lightbox */
    }

    .image-zoom-trigger:hover {
        transform: translateY(-2px);
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
</style>