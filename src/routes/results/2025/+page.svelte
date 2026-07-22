<script>
  import { resolve } from '$app/paths';
</script>

{#snippet footnote(text)}
    <span class="info-trigger" role="button" tabindex="0">
        <span class="info-icon">i</span>
        <span class="tooltip-box">{text}</span>
    </span>
  {/snippet}

<div class="subpage">
  <!-- JUMP MENU -->
  <nav class="jump-menu" aria-label="Report quick links">
    <div class="jump-links">
      <a href="#adult-report" class="jump-btn">Adult Report</a>
      <a href="#paediatric-report" class="jump-btn">Paediatric Report</a>
    </div>
  </nav>

  <div class="accordion-text">
    <p>
      The findings from across 109 adult assessments and 39 paediatric assessments suggest that improvement in ePrescribing safety is achievable, particularly for high-risk medicines, but that local configuration underpinned by leadership and system updates are the primary drivers of performance. The results reinforce the need for close collaboration between users and vendors.
    </p>

    <p>
      The interactive Power BI reports with explanatory notes are provided here for users to review and compare their system results against that of peers from the pooled 2025 data. The primary performance metric is 'good mitigation' defined as where an ePrescribing system correctly identifies a risk of error, providing an appropriate response when a medicine is prescribed.
    </p>

    <p>
      To further support understanding of how to interpret and respond to your ePRaSE results, we recommend the following resources accessible in this website:
    </p>
    <ul>
      <li>
        <a href={resolve("/using")} class="linelink">Responding to ePRaSE</a>: A video presentation by Andrew Heed, Lead Pharmacist for Newcastle Hospitals.
      </li>
      <li>
        <a href={resolve("/lab")} class="linelink">Electronic Prescribing Learning Lab</a>: An interactive resource designed to help digital and pharmacy teams optimise their electronic prescribing systems.
      </li>
    </ul>
  </div>

  <!-- ADULT SECTION -->
  <h2 id="adult-report" class="eprase-h2">V4 2025 Adult Power BI Report</h2>
  <div class="accordion-text">
      <div class="report-container">
        <iframe title="ePRaSE Results Charts v4 Adults final" width="1024" height="612" src="https://app.powerbi.com/view?r=eyJrIjoiMTBhMzE4NTQtMmZmZi00NjNlLWJkNmUtZTg0YTVmMWUwYjM1IiwidCI6IjljNTAxMmM5LWI2MTYtNDRjMi1hOTE3LTY2ODE0ZmJlM2U4NyIsImMiOjh9" frameborder="0" allowFullScreen="true"></iframe>
      </div>
      <p class='highlight'>Page 1: EP System Performance Adults V4 2025</p>

      <!-- EXPLANATORY NOTES ACCORDION (ADULT) -->
      <details class="faq-item notes-accordion">
        <summary class="notes-trigger">
          <span class="trigger-text">Explanatory Notes</span>
        </summary>
        <div class="answer-content">
          <p>This dashboard provides a summary of the number of trusts completing the assessment, data on the overall mitigation performance across all questions and mandatory questions and average numbers of staff{@render footnote("Note the staff average on the summary dashboard is an average of all 109 results; users wishing to see the number of staff data for a particular system can use the system filter to isolate that information.")} that users told us were involved in maintaining their trust EP system. Users can sort the information to benchmark their performance within EP system type using the NHS Trust and system filters on the righthand side of the dashboard using their unique trust and system ID reference numbers.</p>

          <p>The summary of all assessment clinical decision support (CDS) stacked chart illustrates the level of good mitigation in each category. In the main summary chart 'allergy' and 'pregnancy prevention' perform best, indicating that there is good system build in these areas. The pregnancy prevention results shows is clear directional improvement compared to the previous campaign which may reflect user change in approach to Sodium Valproate (an unchanged mandatory high-risk question). Least well performing are 'drug omission' and 'drug laboratory.' The low performance in drug laboratory is likely to reflect the general lack of interoperability reported between laboratory reporting and EP systems.</p>

          <p class='highlight'>Page 2: Good Mitigation Scores Adult V4 2025</p>

          <p>This interactive chart shows the placement of each of the trusts participating in the assessment for 2025. The results are in descending order based on good mitigation scores which is the percentage of potentially unsafe prescription orders that were correctly mitigated. By filtering the data using the dropdown menus at the top of the report or using the colour coded legend circles, users can see there is wide variation in mitigation performance between trusts using the same system. Results strongly suggest there are opportunities for improvement in safety through learning from others' system optimisation.</p>

          <p class='highlight'>Page 3: Good Mitigation Scores by System Adults V4 2025</p>

          <p>In this static chart across all EPMA systems, there is wide variation in mitigation performance between trusts using the same system, often greater than variation between different systems. This suggests that local configuration, optimisation capacity, leadership and governance may be the more dominant determinants of safety mitigation, rather than the underlying vendor platform alone.</p>

          <p class='highlight'>Page 4: Relationship Between Good Mitigation, System Implementation and Last Update Adults V4 2025</p>

          <p>In this static chart across all adult data, newer implementations show better levels of good mitigation.</p>

          <p>More recent updates correlate with marginally better mitigation, stressing the value of consistent update cycles.</p>

          <p>The data suggests an optimal update cycle of 15–20 months, acknowledging that there are many different types of updates.</p>

          <p>Sustaining good mitigation requires combining periodic updates with ongoing oversight and review activities.</p>

          <p class='highlight'>Page 5: Is Your Hospital Laboratory Results System Fully Integrated with Your ePrescribing System? Adult V4 2025</p>

          <p>This chart shows a mixed picture of laboratory and EP system integration between different EP systems and within the same system. For users, data integration is a safety enabler. Limited access to diagnoses and laboratory results in clinical decision support, constrains mitigation potential.</p>

          <p class='highlight'>Page 6: How Do You Describe Penicillin V in Your EP System? Adult V4 2025</p>

          <p>This static chart addresses nationally reported issues around the mis-selection risk (Penicillin vs Penicillamine). Results suggests some improvement - there has been a reduction in the use of Penicillin V between V3 and V4 of ePRaSE. The Approved dm+d name that should be used is Phenoxymethylpenicillin.</p>

          <p class='highlight'>Page 7: Can You Enter Patient Diagnosis and Comorbidities? Adult V4 2025</p>
          <p>This chart shows a mixed picture of systems able to enter and link diagnosis and comorbidities both between different EP systems and within the same system. For users, data integration is a safety enabler. Limited access to diagnoses and comorbidities results in clinical decision support, constrains mitigation potential.</p>

          <p class='highlight'>Page 8: Does your EPMA system have a mechanism in place to automatically identify antimicrobial prescriptions that have reached the review time window e.g. 48-72 hours after initiation? Adult V4 2025</p>
          <p>This slide shows mixed results within EP systems suggesting that some trusts may not recognise their system's capability to meet the Antimicrobial Review Kit (ARK) requirements.</p>
        </div>
      </details>
  </div>

  <!-- PAEDIATRIC SECTION -->
  <h2 id="paediatric-report" class="eprase-h2">V4 2025 Paediatric Power BI Report</h2>
  <div class="accordion-text">
    <div class="report-container">
      <iframe title="ePRaSE Results Charts V4 Paediatrics 25 - final" width="1024" height="612" src="https://app.powerbi.com/view?r=eyJrIjoiOGEwMTljNjUtZGZlYi00MzZjLTlmZDEtMDIyNTJmYTk2NjkwIiwidCI6IjljNTAxMmM5LWI2MTYtNDRjMi1hOTE3LTY2ODE0ZmJlM2U4NyIsImMiOjh9" frameborder="0" allowFullScreen="true"></iframe>
    </div>

    <!-- EXPLANATORY NOTES ACCORDION (PAEDIATRIC) -->
    <details class="faq-item notes-accordion">
      <summary class="notes-trigger">
        <span class="trigger-text">Explanatory Notes</span>
      </summary>
      <div class="answer-content">
        <p class='highlight'>Page 1: EP System Performance Paediatrics V4 2025</p>

        <p>2025 is the first year for paediatric specific questions and results should be understood as a learning phase. This dashboard provides a summary of the number of trusts completing the assessment, data on the overall mitigation performance across all questions, mandatory questions and average numbers of staff{@render footnote("Note the average on the summary dashboard is an average of all 39 results; users wishing to see the number of staff data for a particular system can use the system filter to isolate that information.")} that users told us where involved in maintaining their trust EP system. Users can sort the information to benchmark their performance within EP system type using the NHS trust and system filter on the righthand side of the dashboard using their unique trust and system ID reference numbers.</p>

        <p>The summary of all assessment clinical decision support (CDS) stacked chart illustrates the level of good mitigation in each category.</p>

        <p>Mandatory questions in the paediatric module are different to the adult range. Several paediatric mandatory scenarios (e.g. Methotrexate, Valproate) show low or no red (unmitigated) scores. This performance is similar to, and in places better than, the adult equivalent. Where performance appears weaker (e.g. IV Electrolytes) evidence suggests this reflects deployment choices rather than system limitations.</p>

        <p class='highlight'>Page 2: Good Mitigation Scores Paediatrics V4 2025</p>

        <p>This interactive chart shows the placement of each of the 39 trusts participating in the paediatric assessment for 2025. The results are in descending order based on good mitigation scores which is the percentage of potentially unsafe prescription orders that were correctly mitigated. By filtering the data using the dropdown menus at the top of the report or using the colour coded legend circles, users can see there is wide variation in mitigation performance between trusts using the same system. Results strongly suggest there are opportunities for improvement in safety through learning from others' system optimisation.</p>

        <p class='highlight'>Page 3: Good Mitigation Scores by System Paediatrics V4 2025</p>

        <p>In this static chart across all EPMA systems, there was wide variation in mitigation performance between trusts using the same system, often greater than variation between different systems. This suggests that local configuration, optimisation capacity, leadership and governance may be the more dominant determinants of safety mitigation, rather than the underlying vendor platform alone.</p>

        <p class='highlight'>Page 4: EP System Performance Comparison: Adults (n=109) vs Paediatrics (n=39) V4 2025</p>

        <p>This slide shows when good and some mitigations are combined for paediatrics, overall performance is comparable to adults.</p>

        <p class='highlight'>Page 5: Is Your Hospital Laboratory Results System Fully Integrated with Your ePrescribing System? Paediatrics V4 2025</p>

        <p>This chart shows a mixed picture of laboratory and EP system integration between different EP systems and within the same system. For users, data integration is a safety enabler. Limited access to diagnoses and laboratory results in clinical decision support, constrains mitigation potential.</p>

        <p class='highlight'>Page 6: How Do You Describe Penicillin V in Your EP System? Paediatrics V4 2025</p>

        <p>This static chart addresses nationally reported issues around the mis-selection risk (Penicillin vs Penicillamine). Results suggest 15-20% of the paediatric systems tested still use Penicillin V or a combination of both descriptions; a higher level than reported for adult systems.</p>

        <p>The Approved dm+d name that should be used is Phenoxymethylpenicillin.</p>

        <p class='highlight'>Page 7: Can You Enter Patient Diagnosis and Comorbidities? Paediatrics V4 2025</p>

        <p>This chart shows a mixed picture of systems able to enter and link diagnosis and comorbidities both between different EP systems and within the same system. For users, data integration is a safety enabler. Limited access to diagnoses and comorbidities results in clinical decision support, constrains mitigation potential.</p>

        <p class='highlight'>Page 8: Does your EPMA system have a mechanism in place to automatically identify antimicrobial prescriptions that have reached the review time window e.g. 48-72 hours after initiation? Paediatrics V4 2025</p>

        <p>This slide shows mixed results within EP systems suggesting that some trusts may not recognise their system's capability to meet the Antimicrobial Review Kit (ARK) requirements.</p>
      </div>
    </details>
  </div>
</div>

<style>
    /* Global Smooth Scrolling */
    :global(html) {
        scroll-behavior: smooth;
    }

    /* Anchor layout adjustments underneath sticky jump-menu */
    .eprase-h2 {
        scroll-margin-top: 5rem;
    }

    /* Sticky Jump Menu Container */
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

    .answer-content {
        position: relative;
        padding: 0.5rem 1.5rem 1.5rem 1.5rem;
        background-color: #f8fafc;
        border-top: 1px solid #eef2f6;
        animation: slideDown 0.2s ease-out forwards;
    }

    .answer-content p {
        margin: 1rem 0 0 0;
        font-size: 1.05rem;
        line-height: 1.6;
        color: #4c6272;
    }

    /* Highlights & Tooltips */
    .highlight {
        color: rgb(67, 67, 158);
        font-weight: 600;
    }

    .report-container {
        width: 100%;
        max-width: 1024px;
        margin: 2rem auto;
        aspect-ratio: 16 / 9;
        box-shadow: 0 4px 20px rgba(0,0,0,0.1);
        border-radius: 8px;
        overflow: hidden;
    }
    
    iframe {
        width: 100%;
        height: 100%;
        border: none;
    }

    .tooltip-box {
        visibility: hidden;
        width: 400px;
        max-width: 90vw;
        background-color: var(--nhs-dark-blue);
        color: #fff;
        text-align: left;
        border-radius: 6px;
        padding: 8px;
        position: absolute;
        z-index: 100;
        margin-left: -100px;
        opacity: 0;
        transition: opacity 0.2s ease, transform 0.2s ease;
        font-size: 1.2rem;
        font-weight: normal;
        pointer-events: none;
        box-shadow: 0 4px 12px rgba(0,0,0,0.15);
        bottom: auto;
        left: 120%;
        top: 130%;
        transform: translateY(-50%);
        box-sizing: border-box;
    }

    .tooltip-box::after {
        content: "";
        position: absolute;
        top: 50%;
        right: 100%;
        margin-top: -5px;
        border-style: solid;
        border-color: transparent var(--nhs-dark-blue) transparent transparent;
    }

    .info-trigger {
        position: relative;
        display: inline-flex;
        align-items: center;
        justify-content: center;
        cursor: help;
        margin: 0 4px 12px 4px;
        vertical-align: middle;
    }

    .info-icon {
        width: 18px;
        height: 18px;
        background-color: #FFF;
        color: var(--nhs-blue);
        border: 1px solid var(--nhs-blue);
        border-radius: 50%;
        font-family: "serif";
        font-size: 12px;
        font-weight: bold;
        display: flex;
        align-items: center;
        justify-content: center;
        transition: background-color 0.2s;
    }

    .info-trigger:hover .info-icon,
    .info-trigger:focus .info-icon {
        background-color: #003087;
    }

    .info-trigger:hover .tooltip-box,
    .info-trigger:focus .tooltip-box {
        visibility: visible;
        opacity: 1;
        transform: translateY(-5px); 
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