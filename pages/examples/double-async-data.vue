<template>
  <h1>Double useAsyncData</h1>
  <p><NuxtLink to="/">Home</NuxtLink></p>
  <div v-if="data">
    <ContentRenderer :value="data.page" :key="path" />
    <pre>{{ data.pages.map(page => page.title) }}</pre>
  </div>
</template>

<script lang="ts" setup>
import { useAsyncData } from 'nuxt/app'

const path = '/products'

const { data: page } = await useAsyncData(path, async () => {
  return queryContent(path).findOne()
})

const { data: pages } = await useAsyncData(path + '/pages', async () => {
  return queryContent(path)
    .where({ _path: { $ne: path } })
    .sort({ _path: -1 })
    .find()
})

const data = computed(() => {
  return {
    page: page.value,
    pages: pages.value,
  }
})
</script>
