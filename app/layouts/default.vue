<script setup>
import { computed } from 'vue'
import { useI18n } from 'vue-i18n'

const { locale, locales, setLocale } = useI18n()

const handleLang = (code) => {
  setLocale(code)
  localStorage.setItem('user-locale', code)
}

const isRTL = computed(() => locale.value === 'fa')
</script>

<template>
  <div :dir="isRTL ? 'rtl' : 'ltr'">
    <UContainer>
      <UPageGrid columns="2" gap="4" align="center">
        <div>
          <UButton to="/">Home</UButton>
          <UButton to="/about">About</UButton>
          <UButton to="/publications">Publications</UButton>
          <UButton to="/research">Research</UButton>
          <UButton to="/contact">Contact</UButton>
        </div>
        <div>
          <UButton
            v-for="localeItem in locales"
            :key="localeItem.code"
            :variant="localeItem.code === locale.value ? 'solid' : 'outline'"
            @click="handleLang(localeItem.code)"
          >
            {{ localeItem.name }}
          </UButton>
        </div>
      </UPageGrid>
    </UContainer>
    <slot />
  </div>
</template>