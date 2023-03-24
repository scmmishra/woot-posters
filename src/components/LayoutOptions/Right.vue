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
    <div class="h-[72px] bg-gray-200 grid grid-cols-2 gap-1 p-2">
      <div class="bg-gray-300 rounded-md w-full h-full"></div>
      <div class="space-y-1 pt-1">
        <div class="bg-gray-300 rounded-md w-full h-2"></div>
        <div class="bg-gray-300 rounded-md w-full h-2"></div>
        <div class="bg-gray-300 rounded-md w-full h-2"></div>
      </div>
    </div>
    <div v-if="selected">
      <Checkmark />
    </div>
  </button>
</template>
