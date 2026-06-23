<script lang="ts">
    import { resolve } from '$app/paths';
    import PdfViewer from '$lib/components/PdfViewer.svelte';
</script>
<div class="subpage">
    <p>Read the Learning Lab bibliography below or <a href={resolve("/pdf/ll_bib.pdf")}>download the PDF</a>.</p>

    <PdfViewer src="/pdf/ll_bib.pdf" title="Learning Lab Bibliography" />
</div>