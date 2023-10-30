# Nuxt Content "double await" repro

This repo demonstrates a case where making two `await`ed calls to Content inside `useAsyncData()` fails to return a response. 

It seems to be only the server side, as navigating to the page normally will load content.

Each example page makes two calls to content:

1. load the page content
2. query for related pages

Examples:

- [Double await](/examples/double-await)
  <br>Does not work on server load
- [Double await only calling content once](/examples/double-await-content-once)
  <br>Works as expected
- [Double useAsyncData](/examples/double-async-data)
  <br>Works as expected 
- [Promise.all()](/examples/promise-all)
  <br>Works as expected
