<template>
  <h1>Double await</h1>
  <p class="text-warning">Reload page to see this fail</p>
  <div v-if="data">
    <ContentRenderer :value="data.page" :key="path" />
    <pre>{{ data.pages.map(page => page.title) }}</pre>
  </div>
</template>

<script lang="ts" setup>
import { useAsyncData } from 'nuxt/app'

const path = '/products'

const { data } = await useAsyncData(path + '/double-await', async () => {
  const page = await queryContent(path).findOne()
  const pages = await queryContent(path)
    .where({ _path: { $ne: path } })
    .sort({ _path: -1 })
    .find()
  return {
    page,
    pages,
  }
})
</script>
