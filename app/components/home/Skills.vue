<script setup lang="ts">
const skills = ['Vue', 'Nuxt', 'TypeScript', 'Tailwind', 'NestJS']
</script>

<template>
  <UContainer class="py-20">
    <SectionTitle title="Skills" />

    <div class="flex flex-wrap justify-center gap-4 mt-10">
      <UBadge
        v-for="skill in skills"
        :key="skill"
        color="primary"
        variant="soft"
      >
        {{ skill }}
      </UBadge>
    </div>
  </UContainer>
</template>