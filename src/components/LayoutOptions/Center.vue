<script lang="ts" setup>
import Checkmark from "../Checkmark.vue";
const emit = defineEmits(["select"]);

defineProps<{
  selected: boolean;
}>();

function emitSelected() {
  emit("select");
}
</script>

<template>
  <button
    @click="emitSelected"
    class="rounded-md shadow-lg transform duration-200 transition-transform hover:shadow-xl hover:-translate-y-px overflow-hidden relative"
  >
    <div class="h-[72px] bg-gray-200 flex flex-col gap-2 p-2 pb-0">
      <div class="space-y-1 pt-1">
        <div class="bg-gray-300 rounded-md w-1/2 h-2 mx-auto"></div>
        <div class="bg-gray-300 rounded-md w-full h-2"></div>
      </div>
      <div
        class="bg-gray-300 rounded-md w-5/6 mx-auto h-full rounded-b-none"
      ></div>
    </div>
    <div v-if="selected">
      <Checkmark />
    </div>
  </button>
</template>
