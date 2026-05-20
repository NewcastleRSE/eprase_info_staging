<script>
  import { resolve } from '$app/paths';
</script>
<div class="subpage">
  <p>Results from Version 4 (2025) of the Electronic Prescribing Risk and Safety Evaluation (ePRaSE) tool are now available as interactive, anonymised Power BI reports on the <a href={resolve("/results/2025")} class="linelink">Results 2025 page</a> of this website. Trusts that completed the 2025 assessment have been emailed unique identification numbers, enabling benchmarking against other trusts using the same electronic prescribing (EP) system. Explanatory notes are provided to support interpretation of the data.</p>

  <p>To support interpretation and response to your ePRaSE results, we recommend the following resources:</p>

  <ul>
    <li><a href={resolve("/using")} class="linelink">User experience video</a>: Responding to ePRaSE, Andrew Heed</li>
    <li><a href={resolve("/lab")} class="linelink">Electronic Prescribing Learning Lab</a>: An interactive resource designed to help digital and pharmacy teams optimise their electronic prescribing systems.</li>
  </ul>

  <p>The Learning Lab is an interactive resource designed to help digital and pharmacy teams optimise their electronic prescribing systems.</p>

  <p>The ePRaSE team are already working on the next version of the tool, planned for release early Autumn 2026. If you have not previously had the chance to participate and would like to next time, please register to receive email updates via the QR code below.</p>

  <img class='qrCode' src={resolve("/img/eprase_qr.png")} alt="qr code" />
</div>
<style>
  .qrCode {
    width: 128px;
    margin: 0 auto 2rem auto;
  }
</style>