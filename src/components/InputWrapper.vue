<script setup lang="ts">
defineProps<{
  title: string;
}>();
</script>

<template>
  <div class="space-y-2">
    <h3 class="text-lg font-bold tracking-tight text-gray-700">
      {{ title }}
    </h3>
    <slot></slot>
  </div>
</template>
