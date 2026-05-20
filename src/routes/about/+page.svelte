<script>
	import {resolve} from '$app/paths';
</script>

<div class="subpage">

<p class='topquote'>&quot;Know your risk: an NHS self-assessment for safer ePrescribing.&quot;</p>

<h2>What is ePRaSE?</h2>

<p>The Electronic Prescribing Risk and Safety Evaluation (ePRaSE) is an NHS-led web-based self-assessment tool that helps trusts understand how well their electronic prescribing (EP) systems are configured and maintained to mitigate known prescribing risks.</p>

<p>ePRaSE allows organisations to view their own results immediately to identify potential areas of prescribing risk, and at the end of each annual campaign to benchmark performance against national data. We collaborate with both users and system vendors using aggregated findings from each annual campaign to support shared learning and EP system optimisation across the NHS.</p>

<p>Why take part?</p>
<ul>
	<li>Medicines are one of the highest-volume sources of reported patient-safety incidents.</li>
	<li>ePRaSE provides a structured, evidence-based assessment of how effectively EP systems may prevent high-risk prescribing errors.</li>
 	<li>Trusts receive trust-level reports and national benchmarking to support prioritisation and investment.</li>
	<li>The latest release includes paediatric-specific prescribing scenarios, supporting assessment in this higher-risk area of care.</li>
</ul>

<p>In short, ePRaSE supports proactive risk reduction and continuous improvement in both adult and paediatric prescribing.</p>

<h2>How the tool works</h2>

<p>Trusts are asked to set up a series of fictional patients within their live or test EP environment and complete a structured set of prescribing risk scenarios designed to challenge system safeguards. The tool also includes targeted questions on core safety configuration. Results are generated in real time through an actionable report, supported by visual outputs, to guide optimisation for both established users and new system implementers.</p>

<h2>Help and support</h2>

<p>To support interpretation of results and next steps in the optimisation journey, trusts can access:</p>

<ul>
	<li><a href={resolve("/using")} class="linelink">User experience video</a>: Responding to ePRaSE – Andrew Heed</li>
	<li><a href={resolve("/lab")} class="linelink">Electronic Prescribing Learning Lab</a>: An interactive resource designed to help digital and pharmacy teams optimise their electronic prescribing systems</li>
</ul>

<h2>Who can use ePRaSE?</h2>

<ul>
	<li>Suitable for acute, community, and mental health NHS trusts using or implementing electronic prescribing.</li>
	<li>Includes ability to assess multiple different inpatient EP systems.</li>
	<li>Includes a dedicated paediatric-prescribing safety module.</li>
	<li>Access requires an NHS email address and HSCN connectivity (England or dedicated link for devolved nations).</li>
	<li>Up to four users per trust can register to complete or view the assessment.</li>
</ul>

<p>The ePRaSE application is compatible with all modern web browsers.</p>

<h2>Background</h2>

<p>Electronic prescribing with clinical decision support can reduce medication errors as systems are optimised and users gain experience, but system changes and local variation can introduce new safety risks that are hard to detect. In the UK, ePRaSE was commissioned by NHS England to address the lack of a standard way to evaluate how well ePrescribing systems prevent harm, supporting continuous improvement and optimisation. Since its pilot in 2019, ePRaSE has shown that gaps remain. Early findings indicated only around half of high-risk prescribing scenarios were effectively mitigated, reinforcing the need for ongoing assessment and shared learning. Further details can be found in the open access publication Klein, S., Tsanas, A., Coleman, J. et al. A simulation study to quantitatively assess the performance of electronic prescribing systems in English NHS Hospital Trusts. <em>Sci Rep</em> 15, 1756 (2025). <a class="linelink" href="https://doi.org/10.1038/s41598-025-86112-w">https://doi.org/10.1038/s41598-025-86112-w</a></p>

<p>Recent campaign results for 2024 and 2025 can be found on the <a href={resolve("/results")} class="linelink">Results page</a> of this website.</p>

</div>
<style>
	.topquote {
		font-weight: 400;
    font-size: 2rem;
    font-style: italic;
    text-align: center;
    color: var(--nhs-blue);
	}
</style>
