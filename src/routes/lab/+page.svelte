<script>
    import { resolve } from '$app/paths';
    import PdfViewer from '$lib/components/PdfViewer.svelte';
</script>
<div class="subpage">
    <p>The Electronic Prescribing Learning Lab is an interactive learning resource developed to support digital and pharmacy teams to optimise their electronic prescribing systems. View below or <a href={resolve("/pdf/learning_lab.pdf")} target="_blank">download the PDF</a>.</p>
    <PdfViewer src={resolve("/pdf/learning_lab.pdf")} title="Learning Lab" />
</div>