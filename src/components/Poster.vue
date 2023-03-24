<script lang="ts" setup>
defineProps<{
  title: string;
  body?: string;
  image?: string;
  background: string;
  layout: string;
}>();

let resizeHandler = () => {};

const vAspectRatio = {
  mounted: function (el, binding) {
    // Get the aspect ratio from the binding value
    const aspectRatio = binding.value;

    // Add a resize event listener to the window
    window.addEventListener("resize", resizeHandler);

    // Define the resize handler function
    resizeHandler = () => {
      // Get the width of the parent element
      const parentWidth = el.parentNode.clientWidth;

      // Set the height of the element to maintain the aspect ratio
      el.style.height = `${parentWidth / aspectRatio}px`;
    };

    // Call the resize handler function once to set the initial height
    resizeHandler();
  },
  unmounted: function () {
    // Remove the resize event listener from the window
    window.removeEventListener("resize", resizeHandler);
  },
};
</script>

<template>
  <section
    v-aspect-ratio="1200 / 630"
    id="poster"
    class="bg-white p-8 gap-8"
    :style="{ backgroundImage: `url(/mesh/${background})` }"
    :class="{
      'flex flex-row': layout === 'left',
      'flex flex-row-reverse': layout === 'right',
      'flex flex-col pb-0': layout === 'center',
      'flex flex-col pr-0 pb-0': layout === 'right-break',
    }"
  >
    <div
      :class="{
        'h-full py-5 w-2/5': layout === 'left' || layout === 'right',
        'min-h-20 w-full': layout === 'center' || layout === 'right-break',
      }"
    >
      <h2 class="text-5xl text-white font-bold">{{ title }}</h2>
      <p
        class="text-white text-xl font-normal leading-relaxed mt-5"
        v-if="body"
      >
        {{ body }}
      </p>
    </div>
    <div
      class="w-full bg-white/25 h-full rounded-md backdrop-blur-md border border-white p-2"
      :class="{
        'w-3/5': layout === 'left' || layout === 'right',
        'min-h-20 rounded-b-none':
          layout === 'center' || layout === 'right-break',
        'rounded-tr-none': layout === 'right-break',
      }"
    >
      <div
        v-if="image"
        class="w-full h-full rounded-md bg-cover"
        :style="{ backgroundImage: 'url(' + image + ')' }"
      ></div>
    </div>
  </section>
</template>
