<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'

import { ref } from 'vue'
import { useI18n } from "vue-i18n"
import i18n from "./plugins/i18n"

const selected = ref('')

const languages = ref([
  { language: 'en', title: 'English' },
  { language: 'es', title: 'Español' },
  { language: 'fr', title: 'French' }
])

const { t } = useI18n({
  inheritLocale: true,
  useScope: 'local'
})

const changeLocale = (locale: string) => {
  i18n.global.locale.value = locale
}
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld :msg="t('welcome')" />
      <div class="select">
        <select v-model="selected" @change="changeLocale(selected)">
          <option disabled value="">Select Language</option>
          <option v-for="lang in languages" :key="lang.title" :value="lang.language">
            {{lang.title}}
          </option>

        </select>
      </div>
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  select {
    width: 11rem;
    height: 2rem;
    margin-top: 1rem;
    border: solid green 1px;
    border-radius: 3px;
  }

  input {
    height: 2rem;
    width: 11rem;
    border: solid green 1px;
    border-radius: 3px;
  }

  div.select {
    text-align: center;
  }
}
</style>
