<template>
  <div id="app">
    <nav>
      <NuxtLink to="/">Home</NuxtLink>
    </nav>
    <NuxtPage />
  </div>
</template>

<style>
@import url(https://cdnjs.cloudflare.com/ajax/libs/spectre.css/0.4.5/spectre.min.css);

#app {
  padding: 1rem;
}

ul, ol {
  margin-left: 2rem;
}

li {
  list-style-position: outside;
}
</style>

