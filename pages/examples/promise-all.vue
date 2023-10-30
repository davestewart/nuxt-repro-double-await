<template>
  <h1>Promise.all()</h1>
  <div v-if="data">
    <ContentRenderer :value="data.page" :key="path" />
    <pre>{{ data.pages.map(page => page.title) }}</pre>
  </div>
</template>

<script lang="ts" setup>
import { useAsyncData } from 'nuxt/app'

const path = '/products'

const { data } = await useAsyncData(path + '/promise-all', async () => {
  const [page, pages] = await Promise.all([
    queryContent(path).findOne(),
    queryContent(path)
      .where({ _path: { $ne: path } })
      .sort({ _path: -1 })
      .find()
  ])
  return {
    page,
    pages,
  }
})
</script>
