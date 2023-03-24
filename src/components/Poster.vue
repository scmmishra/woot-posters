<script lang="ts" setup>
defineProps<{
  title: string;
  body?: string;
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
    class="bg-white shadow-lg rounded-lg"
    :style="{ backgroundImage: `url(/mesh/${background})` }"
    :class="{
      'grid grid-cols-2 gap-8 p-8': layout === 'left' || layout === 'right',
      'flex flex-col gap-8 p-8 pb-0': layout === 'center',
      'flex flex-col gap-8 p-8 pr-0 pb-0': layout === 'right-break',
    }"
  >
    <div
      class="w-full rounded-md"
      :class="{
        'h-full py-5': layout === 'left' || layout === 'right',
        'h-20': layout === 'center' || layout === 'right-break',
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
      class="w-full bg-black/25 h-full rounded-md"
      :class="{
        'col-start-1 row-start-1': layout === 'right',
      }"
    ></div>
  </section>
</template>
