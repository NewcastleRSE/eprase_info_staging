<div class="subpage">
<nav class="jump-menu" aria-label="Report quick links">
    <div class="jump-links">
      <a href="#adult-report" class="jump-btn">Power BI Report</a>
      <a href="#masterclass" class="jump-btn">Masterclass Presentation</a>
    </div>
  </nav>
  <div class="accordion-text">
    <p>The 2024 results suggest that people have already done some work with their EP systems, but there are further opportunities to improve and optimise systems to enhance patient safety.</p>

    <p>An interactive Power BI report is provided for users to review and benchmark their system against the pooled data from the 71 trusts that completed the assessment. Registered users will have received an email with their individual trust and system reference numbers to be used when reviewing the information.</p>

    <p>Good mitigation in the ePRaSE tool is defined as where an EP system correctly identifies a risk of error, providing an appropriate response when a medicine is prescribed.</p>

    <h2 id="adult-report">V3 2024 Power BI Report</h2>
    <div class="report-container animate-fade-up">
      <div class="iframe-aspect-wrapper">
        <iframe title="ePRaSE Results Charts - Anonymous for publishing" src="https://app.powerbi.com/view?r=eyJrIjoiZmJjYjI3ZmItMDY1Zi00NGI2LTk3OWMtY2VhM2E2NzYzZjY3IiwidCI6IjljNTAxMmM5LWI2MTYtNDRjMi1hOTE3LTY2ODE0ZmJlM2U4NyIsImMiOjh9" frameborder="0" allowFullScreen="true"></iframe>
      </div> 
    </div>
  </div>

  <!-- EXPLANATORY NOTES ACCORDION -->
  <details class="faq-item notes-accordion">
    <summary class="notes-trigger">
      <span class="trigger-text">Explanatory Notes</span>
    </summary>
    <div class="answer-content">
      <h3>Tab 1: Good Mitigation Score - NHS Trusts</h3>

      <p>This tab shows the placement of each of the trusts participating in the assessment for 2024 in descending order based on good mitigation scores which is the percentage of potentially unsafe prescription orders that were correctly mitigated.</p>

      <p>Users can sort the information to benchmark their performance using either the dropdown filter or legend-coloured circles across the top.</p> 

      <h3>Tab 2: EP System Performance (Dashboard)</h3>

      <p>This tab provides a summary of the number of trusts completing the assessment, data on the overall mitigation performance across all questions and mandatory questions* and average numbers of staff that users told us where involved in maintaining their trust EP system.</p>

      <p>The Clinical Decision Support (CDS) stacked chart illustrates the level of good mitigation in each category. In the main summary chart 'allergy' and 'drug duplication' perform best, indicating that there is good system build in these areas. Least well performing are 'drug omission,' 'drug route' and 'drug labs.'</p>

      <p>Users can sort the information to benchmark their performance within EP system type using the system filter boxes on the righthand side of the dashboard.</p>

      <h4>Mandatory questions</h4>

      <ul>
        <li>Prescribe NovoRapid Insulin prescribed as ml instead of units. This prescription should be prevented.</li>
        <li>Prescribe Methotrexate prescribed for a patient with an inappropriate frequency e.g., 10mg daily. This prescription should be prevented.</li>
        <li>Sodium Valproate prescribed in woman of child-bearing age. Pregnancy Prevention Programme requirements must be met due to teratogenic risk. Prescription can be completed with system/user intervention.</li>
        <li>Topiramate initiated in women of childbearing potential with positive pregnancy test. Pregnancy Prevention Programme requirements must be met due to teratogenic risk. Prescription can be completed with system/user intervention.</li>
      </ul>

      <p>Please note Glargine Solostar question, we are not including results in our main analysis because the ePRaSE team understand that users found the test difficult to interpret. This will be improved in the next version.</p>

      <h3>Tab 3: Average Mitigation Score Across EP Systems</h3>

      <p>This tab allows users to compare average scores for good mitigation across all the system types. For context, the number of trusts undertaking the assessment in system type is provided in the 'System Count' column of the table provided.</p>

      <h3>Tab 4: Lab Integration Within EP system</h3>

      <p>This tab provides an overview of what users told us about integration of their hospital laboratory systems with their EP system. Users with systems currently not integrated can assess with what they already know about their system what may or may not be achievable in the future.</p>

      <h3>Tab 5: Description of Penicillin in EP systems</h3>

      <p>This tab shows the results of a question on the description of Phenoxymethylpenicillin in user EP systems. Using the description Penicillin V may lead to the mis-selection of Penicillamine as an allergy status. Users can verify that they are using the correct dm+d description and compare data within their system type.</p>
    </div>
  </details>

  <h2 id="masterclass">Online Presentation: ePRaSE 2024 Rollout</h2>
  <div class="accordion-text">
    <div class="eprase-video">
      <div class="iframe-aspect-wrapper">
        <iframe 
          src="https://www.youtube.com/embed/fsZRF-xW28Y" 
          title="YouTube video player" 
          frameborder="0" 
          allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" 
          referrerpolicy="strict-origin-when-cross-origin" 
          allowfullscreen>
        </iframe>
      </div>
    </div>
  </div>
</div>

<style>
    h2 {
      scroll-margin-top: 5rem;
    }

    .jump-menu {
        position: sticky;
        top: 0;
        z-index: 100;
        background: rgba(255, 255, 255, 0.95);
        backdrop-filter: blur(8px);
        border-bottom: 1px solid #d8dde2;
        padding: 1rem;
        margin-bottom: 1.5rem;
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 1rem;
    }

    .jump-links {
        display: flex;
        gap: 0.5rem;
        flex-wrap: wrap;
        justify-content: center;
    }

    /* Pill Buttons */
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

    .jump-btn:hover {
        background-color: var(--nhs-blue);
        color: #ffffff;
        box-shadow: 0 2px 6px rgba(0, 94, 184, 0.2);
    }
    /* Accordion Style Adaptations */
    .notes-accordion {
        margin: 2rem 0;
        border: 1px solid #d8dde2;
        background: #ffffff;
        border-radius: 8px;
        overflow: hidden;
        transition: border-color 0.2s, box-shadow 0.2s;
    }

    .notes-accordion:hover {
        border-color: #005EB8;
        box-shadow: 0 2px 8px rgba(0, 94, 184, 0.05);
    }

    .notes-accordion[open] {
        border-color: #005EB8;
        box-shadow: 0 4px 12px rgba(0, 50, 135, 0.08);
    }

    /* Summary bar setup */
    .notes-trigger {
        padding: 1.25rem 1.5rem;
        cursor: pointer;
        list-style: none;
        display: flex;
        align-items: center;
        user-select: none;
    }

    .notes-trigger::-webkit-details-marker {
        display: none;
    }

    .trigger-text {
        font-size: 1.25rem;
        font-weight: 600;
        color: #003087;
    }

    .notes-trigger::after {
        content: "＋ View Notes";
        margin-left: auto;
        font-size: 0.9rem;
        font-weight: 700;
        color: #005EB8;
        background: #f0f4f8;
        padding: 0.4rem 0.8rem;
        border-radius: 12px;
        transition: all 0.2s ease;
    }

    .notes-accordion[open] .notes-trigger::after {
        content: "－ Hide Notes";
        background: #005EB8;
        color: #ffffff;
    }

    /* Inner text container */
    .answer-content {
        padding: 0.5rem 2rem 2rem 2rem;
        background-color: #f8fafc;
        border-top: 1px solid #eef2f6;
        animation: slideDown 0.2s ease-out forwards;
    }

    /* Target headers inside the active accordion with clean margins */
    .answer-content h3 {
        color: #003087;
        margin: 1.75rem 0 0.5rem 0;
        font-size: 1.2rem;
        font-weight: 700;
    }

    /* Set first header to have no top padding */
    .answer-content h3:first-of-type {
        margin-top: 1rem;
    }

    .answer-content h4 {
        color: #4c6272;
        margin: 1.25rem 0 0.5rem 0;
        font-size: 1.05rem;
        font-weight: 700;
    }

    .answer-content p {
        margin: 0 0 1rem 0;
        font-size: 1.05rem;
        line-height: 1.6;
        color: #4c6272;
    }

    .answer-content p:last-child {
        margin-bottom: 0;
    }

    /* Bullet point formatting within accordion */
    .answer-content ul {
        margin: 0 0 1rem 1.5rem;
        padding: 0;
    }

    .answer-content li {
        margin-bottom: 0.5rem;
        font-size: 1.05rem;
        line-height: 1.5;
        color: #4c6272;
    }

    .report-container, .eprase-video {
        width: 100%;
        max-width: 1024px;
        margin: 2rem auto;
        box-shadow: 0 4px 20px rgba(0,0,0,0.1);
        border-radius: 8px;
        overflow: hidden;
    }

    .iframe-aspect-wrapper {
        position: relative;
        width: 100%;
        padding-bottom: 56.25%; /* 16:9 Aspect Ratio */
        height: 0;
    }

    .iframe-aspect-wrapper iframe {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        border: none;
    }

    @keyframes slideDown {
        from {
            opacity: 0;
            transform: translateY(-4px);
        }
        to {
            opacity: 1;
            transform: translateY(0);
        }
    }
</style>