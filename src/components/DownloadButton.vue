<script lang="ts" setup>
import html2canvas from "html2canvas";

function downloadPoster() {
  const poster = document.getElementById("poster") as HTMLElement;
  html2canvas(poster, { scale: 5 }).then(function (canvas) {
    canvas.toBlob(
      (blob) => {
        const anchor = document.createElement("a");
        anchor.download = "poster.jpg";
        anchor.href = URL.createObjectURL(blob as Blob);

        anchor.click();

        URL.revokeObjectURL(anchor.href);
      },
      "image/png",
      1
    );
  });
}
</script>
<template>
  <button
    @click="downloadPoster"
    class="px-12 rounded-md bg-gray-300 hover:text-black py-4 text-gray-800 text-xl font-bold"
  >
    Download Poster
  </button>
</template>
