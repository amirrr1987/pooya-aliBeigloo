<script setup lang="ts">
import { computed } from 'vue'
import { useI18n } from 'vue-i18n'

const { locale, getLocaleMessage } = useI18n()
const messages = computed(() => getLocaleMessage(locale.value))
const profile = computed(() => messages.value.personal || {})
const position = computed(() => messages.value.current_position || {})
const academicProfiles = computed(() => messages.value.academic_profiles || {})
const collaborators = computed(() => messages.value.collaborators_sample || [])
const applications = computed(() => messages.value.applications || [])
</script>

<template>
  <UContainer>
    <UPageGrid columns="2" gap="4">
      <UCard>
        <template #header>
          <h1>{{ profile.full_name }}</h1>
        </template>
        <p>{{ profile.title }}</p>
        <p>{{ profile.affiliation }}</p>
        <p>{{ profile.department }}</p>
        <p>{{ profile.location }}</p>
      </UCard>

      <UCard>
        <template #header>
          <h2>Current position</h2>
        </template>
        <p><strong>{{ position.role }}</strong></p>
        <p>{{ position.lab }}</p>
        <p>{{ position.institution }}</p>
      </UCard>
    </UPageGrid>

    <UPageGrid columns="2" gap="4">
      <UCard>
        <template #header>
          <h2>Academic profiles</h2>
        </template>
        <UPageGrid columns="1" gap="2">
          <UButton v-if="academicProfiles.google_scholar" :href="academicProfiles.google_scholar" target="_blank" rel="noreferrer" variant="outline">
            Google Scholar
          </UButton>
          <UButton v-if="academicProfiles.researchgate" :href="academicProfiles.researchgate" target="_blank" rel="noreferrer" variant="outline">
            ResearchGate
          </UButton>
          <UButton v-if="academicProfiles.academia" :href="academicProfiles.academia" target="_blank" rel="noreferrer" variant="outline">
            Academia
          </UButton>
          <UButton v-if="academicProfiles.ad_scientific_index" :href="academicProfiles.ad_scientific_index" target="_blank" rel="noreferrer" variant="outline">
            AD Scientific Index
          </UButton>
        </UPageGrid>
      </UCard>

      <UCard>
        <template #header>
          <h2>Collaboration & applications</h2>
        </template>
        <p>Current collaborators:</p>
        <ul>
          <li v-for="partner in collaborators" :key="partner">{{ partner }}</li>
        </ul>
        <p>Application areas:</p>
        <UPageGrid columns="2" gap="2">
          <UBadge v-for="item in applications" :key="item">{{ item }}</UBadge>
        </UPageGrid>
      </UCard>
    </UPageGrid>
  </UContainer>
</template>
