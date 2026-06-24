<script>
    import { resolve } from '$app/paths';
    import PdfViewer from '$lib/components/PdfViewer.svelte';
</script>
<div class="subpage">
    <p>Step-by-step instructions for using the ePRaSE tool can be found in <a class="linelink" target="_blank" href={resolve("/pdf/EpraseUserGuide2025.pdf")} title="User Guide PDF">this PDF file</a>.</p>

    <PdfViewer src="/pdf/EpraseUserGuide2025.pdf" title="User Guide" />
</div>