<script>
    import { resolve } from '$app/paths';
</script>

<div class="subpage">
    <nav class="jump-menu" aria-label="Team member quick links">
        <div class="jump-links">
            <a href="#ann" class="jump-btn">Ann Slee</a>
            <a href="#neil" class="jump-btn">Neil Watson</a>
            <a href="#jamie" class="jump-btn">Jamie Coleman</a>
            <a href="#stephen" class="jump-btn">Stephen Tomlin</a>
            <a href="#stephanie" class="jump-btn">Stephanie Klein</a>
            <a href="#becky" class="jump-btn">Rebecca Osselton</a>
        </div>
    </nav>
    <div class="team-container">

        <div id="ann" class="bio-card">
            <div class="image-wrapper">
                <img src={resolve("/img/team/ann.webp")} alt="Ann Slee" class="bio-image" />
            </div>
            <div class="bio-content">
                <h2>Ann Slee</h2>
                <span class="role-badge">ePRaSE Programme Chair</span>
                <p>Ann is a highly experienced clinical informatics leader, pharmacist, and former Director of Hospital Pharmacy. She has led national and international digital medicines and ePrescribing programmes, including the development of interoperability standards, the expansion of the Electronic Prescription Service (EPS), and the use of ePMA data for research. Ann has championed the implementation of ePMA systems across the NHS and led the development of the ePrescribing Toolkit, ePRaSE, and the Learning Lab. A Fellow of the Royal Pharmaceutical Society and the British Computer Society, she received the UKCPA Outstanding Achievement Award in 2022.</p>
            </div>
        </div>

        <div id="neil" class="bio-card">
            <div class="image-wrapper">
                <img src={resolve("/img/team/neil.webp")} alt="Neil W Watson" class="bio-image" />
            </div>
            <div class="bio-content">
                <h2>Neil W Watson</h2>
                <span class="role-badge">Programme SRO</span>
                <p>Neil is Director of Innovation at The Newcastle upon Tyne Hospitals NHS Foundation Trust and former Director of Pharmacy. He led the North East and North Cumbria COVID-19 Vaccination Programme, driving innovative approaches to address health inequalities. His interests include advanced therapies, genomics, population health, and clinical informatics to support healthcare transformation. Since 2018, he has been Co-Director of the Northern Alliance Advanced Therapies Treatment Centre, helping integrate advanced therapies into the NHS. He is also a member of the Rare Disease Research UK Hub, contributing NHS expertise to advance research and innovation.</p>
            </div>
        </div>

        <div id="jamie" class="bio-card">
            <div class="image-wrapper">
                <img src={resolve("/img/team/jamie.webp")} alt="Jamie J Coleman" class="bio-image" />
            </div>
            <div class="bio-content">
                <h2>Jamie J Coleman</h2>
                <span class="role-badge">Clinical Leadership</span>
                <p>Jamie is a Consultant Physician at University Hospitals Birmingham, Honorary Professor in Clinical Pharmacology at the University of Birmingham, and Associate Medical Director with responsibility for Medicines Management and safer medicines practice. He leads Hypertension Services at Queen Elizabeth Hospital, directs the West Midlands Yellow Card Centre, and chairs the MHRA Pharmacovigilance Expert Advisory Group as a Commissioner on Human Medicines. A recognised expert in medicines safety and electronic prescribing, Jamie has published over 150 peer-reviewed papers, authored the <em>Oxford Handbook of Practical Drug Therapy</em>, and chairs the adult Clinical Reference Group for the ePRaSE programme.</p>
            </div>
        </div>

        <div id="stephen" class="bio-card">
            <div class="image-wrapper">
                <img src={resolve("/img/team/stephen.webp")} alt="Stephen Tomlin" class="bio-image" />
            </div>
            <div class="bio-content">
                <h2>Stephen Tomlin</h2>
                <span class="role-badge">Clinical and Safety Advisor</span>
                <p>Stephen has over 30 years' experience in children's medicines and became the UK's first Paediatric Consultant Pharmacist in 2007. He is now Director of the Children's Medicines Research & Innovation Centre at Great Ormond Street Hospital, following three years as Chief Pharmacist. As Professional Lead of the Neonatal and Paediatric Pharmacists Group and Chair of the Joint Medicines Committee at the Royal College of Paediatrics and Child Health, he represents paediatric pharmacy nationally, including at government and media level. Passionate about advancing paediatric medicines, he also leads the paediatric clinical reference group within ePRaSE.</p>
            </div>
        </div>

        <div id="stephanie" class="bio-card">
            <div class="image-wrapper">
                <img src={resolve("/img/team/stephanie.webp")} alt="Stephanie Klein" class="bio-image" />
            </div>
            <div class="bio-content">
                <h2>Stephanie Klein</h2>
                <span class="role-badge">ePRaSE Programme Manager</span>
                <p>Stephanie Klein is a senior NHS pharmacy leader and Programme Manager for ePRaSE, specialising in medicines safety, digital transformation, and large-scale healthcare change. She leads work to improve prescribing safety and governance through digital innovation across NHS organisations. With over 30 years' experience spanning clinical pharmacy, aseptic and production services, operational leadership, and system-wide transformation, she has held senior roles in oncology, paediatrics, pharmacy production and emergency healthcare programmes, including the NHS COVID-19 Vaccination Programme and Nightingale Hospital North East. Her special interests include medicines safety, patient safety, clinical governance, digital health and quality improvement. </p>
            </div>
        </div>

        <div id="becky" class="bio-card">
            <div class="image-wrapper">
                <img src={resolve("/img/team/becky.webp")} alt="Becky Osselton" class="bio-image" />
            </div>
            <div class="bio-content">
                <h2>Rebecca Osselton</h2>
                <span class="role-badge">ePRaSE Technical Lead</span>
                <p>Rebecca Osselton is a Senior Research Software Engineer in Newcastle University's RSE team and helps direct the technical development of the tool. She became involved in the ePRaSE project six years ago when the application was at an early prototype stage. She took over the main development work for a few years, before taking a more management-focused role in the project. She attends board meetings and works closely with the team at Newcastle University to deliver the application successfully.</p>
            </div>
        </div>
    </div>
</div>

<style>
    .team-container {
        max-width: 900px;
        margin: 0 auto;
        display: flex;
        flex-direction: column;
        gap: 2rem;
        padding: 1rem 0;
    }

    /* Elegant, Split-Layout Box */
    .bio-card {
        background: #ffffff;
        border: 1px solid #d8dde2;
        border-radius: 12px;
        padding: 2rem;
        display: flex;
        flex-direction: column; /* Stacked on mobile */
        align-items: center;
        gap: 2rem;
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.02);
        scroll-margin-top: 5rem; 
    }

    /* Centered alignment control for image on mobile scaling */
    .image-wrapper {
        flex-shrink: 0;
        display: flex;
        justify-content: center;
    }

    .bio-image {
        width: 140px;
        height: 140px;
        border-radius: 50%;
        object-fit: cover;
        border: 4px solid #ffffff;
        /* Sleek dual-ring border design using box shadow tokens */
        box-shadow: 0 0 0 2px var(--nhs-blue), 0 6px 16px rgba(0, 94, 184, 0.1);
    }

    /* Typography layout */
    .bio-content {
        flex: 1;
        text-align: center; /* Centered on mobile */
    }

    .bio-content h2 {
        margin: 0 0 0.25rem 0;
        font-size: 1.6rem;
        color: var(--nhs-dark-blue);
        font-weight: 700;
    }

    /* Subtle descriptor label below name */
    .role-badge {
        display: inline-block;
        font-size: 0.9rem;
        font-weight: 600;
        color: var(--nhs-blue);
        margin-bottom: 1rem;
        letter-spacing: 0.02em;
    }

    .bio-content p {
        margin: 0;
        font-size: 1.05rem;
        line-height: 1.6;
        color: #4c6272;
    }

    /* Enable smooth scrolling for jump targets */
    :global(html) {
        scroll-behavior: smooth;
    }

    /* Sticky Jump Menu Container */
    .jump-menu {
        position: sticky;
        top: 0;
        z-index: 100;
        background: rgba(255, 255, 255, 0.95);
        backdrop-filter: blur(8px); /* Modern frosted-glass effect */
        border-bottom: 1px solid #d8dde2;
        padding: 1rem;
        margin-bottom: 1.5rem;
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 1rem;
    }

    .jump-title {
        font-size: 0.85rem;
        font-weight: 700;
        color: #4c6272;
        text-transform: uppercase;
        letter-spacing: 0.05em;
    }

    .jump-links {
        display: flex;
        gap: 0.5rem;
        flex-wrap: wrap; /* Wraps cleanly to a second row on small mobile screens */
        justify-content: center;
    }

    /* Pill-Style Jump Buttons */
    .jump-btn {
        display: inline-block;
        padding: 0.5rem 1rem;
        font-size: 0.9rem;
        font-weight: 600;
        color: var(--nhs-blue);
        text-decoration: none;
        background-color: #f0f4f8;
        border: 1px solid transparent;
        border-radius: 20px;
        transition: all 0.2s ease;
    }

    /* Interactive States */
    .jump-btn:hover {
        background-color: var(--nhs-blue);
        color: #ffffff;
        box-shadow: 0 2px 6px rgba(0, 94, 184, 0.2);
    }

    .jump-btn:active {
        transform: scale(0.97);
    }

    /* --- RESPONSIVE DESKTOP DESIGNS --- */
    @media (min-width: 680px) {
        .bio-card {
            flex-direction: row; /* Snaps image to left, text to right */
            align-items: flex-start;
            padding: 2.5rem;
        }

        .bio-content {
            text-align: left; /* Restores clean reading alignment */
        }
    }
</style>