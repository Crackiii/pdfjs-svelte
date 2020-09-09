<script>
  import { onMount } from "svelte";
</script>

<style>
  :global(body) {
    margin: 0;
    padding: 0;
  }
  .iframe {
    width: 100vw;
    height: 100vh;
    border: none;
  }
</style>

<iframe
  src="./pdfjs-dist/web/viewer.html?file=ford.pdf"
  title="vidy"
  class="iframe" />
