<template>
  <h1>Double await</h1>
  <div v-if="data">
    <ContentRenderer :value="data.page" :key="path" />
    <pre>{{ data.pages.map(page => page.title) }}</pre>
  </div>
</template>

<script lang="ts" setup>
import { useAsyncData } from 'nuxt/app'

const path = '/products'

function test () {
  return new Promise(function (resolve, reject) {
    resolve([
      { title: 'Foo' },
      { title: 'Bar' },
      { title: 'Baz' },
    ])
  })
}

const { data } = await useAsyncData(path + '/double-await-content-once', async () => {
  const page = await queryContent(path).findOne()
  const pages = await test()
  return {
    page,
    pages,
  }
})
</script>
