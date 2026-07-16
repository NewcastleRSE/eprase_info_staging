
<div class="subpage">
    <p>Thanks for your interest in the ePRaSE project. Your thoughts and enquiries are important to us.</p>
    
    <div class="contact-grid">
        <div class="contact-card">
            <div class="card-icon font-icon email-icon">✉</div>
            <div class="card-content">
                <h2>General Enquiries</h2>
                <p>For project information, feedback, or general support.</p>
                <a class="linelink" href="mailto:nuth.eprase@nhs.net">
                    nuth.eprase@nhs.net
                </a>
            </div>
        </div>

        <div class="contact-card">
            <div class="card-icon font-icon">📰</div>
            <div class="card-content">
                <h2>Media & Press</h2>
                <p class="contact-person"><strong>Laura Keen</strong></p>
                <a class="linelink" href="mailto:nuth.eprase@nhs.net">
                    nuth.eprase@nhs.net
                </a>
            </div>
        </div>

        <div class="contact-card">
            <div class="card-icon font-icon">🌐</div>
            <div class="card-content">
                <h2>Social Media</h2>
                <p>Follow our updates and engage with the ePRaSE community.</p>
                <a class="linelink" href="https://www.linkedin.com/company/eprase" target="_blank" rel="noopener noreferrer">
                    Connect on LinkedIn
                </a>
            </div>
        </div>
    </div>
</div>

<style>
    /* Global design tokens aligned with NHS Digital guidelines */
    :thin {
        --nhs-blue: #005EB8;
        --nhs-dark-blue: #003087;
        --nhs-secondary-text: #4c6272;
        --border-color: #e8edf1;
        --bg-light: #f8fabd;
    }

    /* Layout Grid */
    .contact-grid {
        display: flex;
        flex-direction: column;
        gap: 1.25rem;
    }

    /* Clean Card Style */
    .contact-card {
        display: flex;
        align-items: flex-start;
        gap: 1.25rem;
        padding: 1.5rem;
        background: #ffffff;
        border: 1px solid #d8dde2;
        border-radius: 8px;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.02);
        transition: transform 0.2s, box-shadow 0.2s, border-color 0.2s;
    }

    .contact-card:hover {
        border-color: #005EB8;
        box-shadow: 0 4px 12px rgba(0, 94, 184, 0.08);
        transform: translateY(-2px);
    }

    /* Left-side Icon accents */
    .card-icon {
        font-size: 1.75rem;
        background: #f0f4f9;
        width: 50px;
        height: 50px;
        display: flex;
        align-items: center;
        justify-content: center;
        border-radius: 50%;
        color: #005EB8;
        flex-shrink: 0;
    }

    .email-icon {
        font-size: 3rem; 
        padding-bottom: 5px; /* Optional: nudges it slightly if it sits too low */
    }

    .card-content {
        flex: 1;
    }

    .card-content h2 {
        margin: 0 0 0.5rem 0;
        font-size: 1.35rem;
        font-weight: 600;
        color: #003087;
    }

    .card-content p {
        margin: 0 0 1rem 0;
        font-size: 1rem;
        line-height: 1.5;
        color: #4c6272;
    }

    .contact-person {
        color: #212b32 !important;
    }

    /* Premium Link Interactions */
    .contact-link {
        display: inline-flex;
        align-items: center;
        font-weight: 600;
        color: #005EB8;
        text-decoration: none;
        border-bottom: 2px solid transparent;
        padding-bottom: 2px;
        transition: color 0.2s, border-color 0.2s;
        word-break: break-all;
    }

    .contact-link:hover {
        color: #003087;
        border-color: #003087;
    }

    /* Optional link specific decorations */
    .mail-link::before {
        content: "✉ ";
        margin-right: 4px;
        font-weight: normal;
    }
    
    .external-link::after {
        content: " ↗";
        font-weight: normal;
        margin-left: 4px;
    }

    /* Responsive Grid Tweak */
    @media (min-width: 650px) {
        .contact-grid {
            display: grid;
            grid-template-columns: 1fr; /* Stacked layout fits nicely, but can expand to 2-columns if content grows */
        }
    }
</style>