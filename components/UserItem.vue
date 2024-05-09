<script setup lang="ts">
const name = ref("Bong Kim");
const description = ref("無名な地球人");
</script>

<template>
  <div class="m-2 p-4 border rounded flex items-center justify-start gap-2">
    <div
      class="rounded-full w-10 h-10 bg-green-500 flex items-center justify-center font-bold text-white"
    >
      {{ name[0] }}
    </div>
    <div>
      <p class="m-0 text-sm text-black font-bold leading-1">{{ name }}</p>
      <p class="m-0 text-xs">{{ description }}</p>
    </div>
  </div>
</template>

<style scoped></style>
