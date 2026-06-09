<script setup lang="ts">
defineProps<{ title: string; subtitle?: string }>()
</script>

<template>
  <div class="text-center max-w-2xl mx-auto">
    <h2 class="text-3xl font-bold">{{ title }}</h2>
    <p
      v-if="subtitle"
      class="text-gray-400 mt-2"
    >
      {{ subtitle }}
    </p>
  </div>
</template>