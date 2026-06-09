<script setup lang="ts">
import { computed } from 'vue'
import { useI18n } from 'vue-i18n'

const { locale, getLocaleMessage } = useI18n()
const messages = computed(() => getLocaleMessage(locale.value))
const profile = computed(() => messages.value.personal || {})
const metrics = computed(() => messages.value.metrics || {})
const fields = computed(() => messages.value.research_fields || [])
const publications = computed(() => messages.value.top_publications || [])
const position = computed(() => messages.value.current_position || {})
const summary = computed(() => messages.value.research_focus_summary || '')
</script>

<template>
  <UContainer>
    <UCard>
      <template #header>
        <div>
          <h1>{{ profile.full_name }}</h1>
          <p>{{ profile.title }} · {{ profile.affiliation }}</p>
          <p>{{ profile.department }} · {{ profile.location }}</p>
        </div>
      </template>

      <UPageGrid columns="2" gap="4">
        <UCard>
          <template #header>
            <h2>About</h2>
          </template>
          <p>{{ summary }}</p>
          <p>
            <strong>{{ position.role }}</strong>
            · {{ position.lab }}, {{ position.institution }}
          </p>
        </UCard>

        <UCard>
          <template #header>
            <h2>Key metrics</h2>
          </template>
          <UPageGrid columns="2" gap="3">
            <div>
              <strong>{{ metrics.publications_count }}</strong>
              <p>Publications</p>
            </div>
            <div>
              <strong>{{ metrics.citations }}</strong>
              <p>Citations</p>
            </div>
            <div>
              <strong>{{ metrics.h_index }}</strong>
              <p>h-index</p>
            </div>
            <div>
              <strong>{{ metrics.i10_index }}</strong>
              <p>i10-index</p>
            </div>
            <div>
              <strong>{{ metrics.reads }}</strong>
              <p>Reads</p>
            </div>
          </UPageGrid>
        </UCard>
      </UPageGrid>

      <UPageGrid columns="3" gap="3">
        <UButton color="primary" to="/research">Research</UButton>
        <UButton color="secondary" to="/publications">Publications</UButton>
        <UButton variant="outline" to="/contact">Contact</UButton>
      </UPageGrid>
    </UCard>

    <UPageGrid columns="2" gap="4">
      <UCard>
        <template #header>
          <h2>Research fields</h2>
        </template>
        <UPageGrid columns="2" gap="2">
          <UBadge v-for="field in fields" :key="field">{{ field }}</UBadge>
        </UPageGrid>
      </UCard>

      <UCard>
        <template #header>
          <h2>Recent publications</h2>
        </template>
        <ul>
          <li v-for="pub in publications.slice(0, 4)" :key="pub.title">
            <strong>{{ pub.title }}</strong>
            <div>{{ pub.year }} · {{ pub.journal || pub.type }}</div>
          </li>
        </ul>
      </UCard>
    </UPageGrid>
  </UContainer>
</template>