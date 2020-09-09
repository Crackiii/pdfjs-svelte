<script>
  import PdfViewer from "./pdf-viewer/viewer.svelte";
  // const src = "./Nadeem_Ahmad_U.pdf";
  const src =
    new URLSearchParams(location.search).get("src") || "./Nadeem_Ahmad_U.pdf";
</script>

<PdfViewer {src} />
