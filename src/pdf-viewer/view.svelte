<script>
  import { onMount } from "svelte";
  import pdfjs from "pdfjs-dist";
  import pdfjsWorker from "pdfjs-dist/build/pdf.worker.entry";
  //   import pdfjsViewer from "pdfjs-dist/web/pdf_viewer.js";
  export const src = "";
  pdfjs.GlobalWorkerOptions = pdfjsWorker;
  var loadingTask = pdfjs.getDocument(src);
  loadingTask.promise.then(function (pdf) {
    var __TOTAL_PAGES = pdf.numPages;
    // Fetch the first page
    var pageNumber = 1;
    for (let i = 1; i <= __TOTAL_PAGES; i += 1) {
      var id = "the-canvas" + i;
      document
        .querySelector("#canvas_div")
        .insertAdjacentHTML(
          "beforeend",
          "<div style='background-color:gray;text-align: center;padding:20px;' ><canvas calss='the-canvas' id='" +
            id +
            "'></canvas></div>"
        );
      var canvas = document.getElementById(id);
      //var pageNumber = 1;
      renderPage(canvas, pdf, pageNumber++, function pageRenderingComplete() {
        if (pageNumber > pdf.numPages) {
          return;
        }
        // Continue rendering of the next page
        renderPage(canvas, pdf, pageNumber++, pageRenderingComplete);
      });
    }
  });
  function renderPage(canvas, pdf, pageNumber, callback) {
    pdf.getPage(pageNumber).then(function (page) {
      var scale = 1.5;
      var viewport = page.getViewport({ scale: scale });
      var pageDisplayWidth = viewport.width;
      var pageDisplayHeight = viewport.height;
      //var pageDivHolder = document.createElement();
      // Prepare canvas using PDF page dimensions
      //var canvas = document.createElement(id);
      var context = canvas.getContext("2d");
      canvas.width = pageDisplayWidth;
      canvas.height = pageDisplayHeight;
      // pageDivHolder.appendChild(canvas);
      // Render PDF page into canvas context
      var renderContext = {
        canvasContext: context,
        viewport: viewport,
      };
      page.render(renderContext).promise.then(callback);
    });
  }
</script>

<div id="container" />
