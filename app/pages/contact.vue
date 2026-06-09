<script setup lang="ts">
import { computed, ref } from 'vue'
import { useI18n } from 'vue-i18n'

const { locale, getLocaleMessage } = useI18n()
const messages = computed(() => getLocaleMessage(locale.value))
const academicProfiles = computed(() => messages.value.academic_profiles || {})
const name = ref('')
const email = ref('')
const message = ref('')
const showModal = ref(false)
const submitted = ref(false)

const handleSubmit = () => {
  if (name.value && email.value && message.value) {
    showModal.value = true
  }
}

const confirmSend = () => {
  submitted.value = true
  showModal.value = false
  name.value = ''
  email.value = ''
  message.value = ''
}
</script>

<template>
  <UContainer>
    <UCard>
      <template #header>
        <h1>Contact</h1>
      </template>
      <p>Please use the form below to get in touch.</p>
      <UForm @submit.prevent="handleSubmit">
        <UFormGroup label="Name">
          <UInput v-model="name" placeholder="Your name" />
        </UFormGroup>
        <UFormGroup label="Email">
          <UInput v-model="email" type="email" placeholder="Your email" />
        </UFormGroup>
        <UFormGroup label="Message">
          <UTextarea v-model="message" placeholder="Your message" rows="5" />
        </UFormGroup>
        <UButton type="submit" color="primary">Send message</UButton>
      </UForm>
      <UPageGrid columns="2" gap="3">
        <UCard>
          <template #header>
            <h2>Profiles</h2>
          </template>
          <UButton v-if="academicProfiles.google_scholar" :href="academicProfiles.google_scholar" target="_blank" rel="noreferrer" variant="outline">
            Google Scholar
          </UButton>
          <UButton v-if="academicProfiles.researchgate" :href="academicProfiles.researchgate" target="_blank" rel="noreferrer" variant="outline">
            ResearchGate
          </UButton>
        </UCard>
        <UCard>
          <template #header>
            <h2>More links</h2>
          </template>
          <UButton v-if="academicProfiles.academia" :href="academicProfiles.academia" target="_blank" rel="noreferrer" variant="outline">
            Academia
          </UButton>
          <UButton v-if="academicProfiles.ad_scientific_index" :href="academicProfiles.ad_scientific_index" target="_blank" rel="noreferrer" variant="outline">
            AD Scientific Index
          </UButton>
        </UCard>
      </UPageGrid>
      <UAlert v-if="submitted" variant="success">
        Your message has been submitted. Thank you!
      </UAlert>
    </UCard>

    <UModal v-model:show="showModal">
      <template #header>
        <h2>Confirm message</h2>
      </template>
      <p>Review your message before sending it.</p>
      <UButton color="primary" @click="confirmSend">Confirm</UButton>
      <UButton variant="outline" @click="showModal = false">Cancel</UButton>
    </UModal>
  </UContainer>
</template>
