<template>
  <main>
    <nav class="container flex justify-between px-2 py-8 mx-auto">
      <nuxt-link to="/">
        Home
      </nuxt-link>
      <div>
        <nuxt-link to="/sobre">
          Sobre
        </nuxt-link>
      </div>
    </nav>
    <nuxt />
  </main>
</template>

<style>
p {
  @apply mb-2
}
h1, h2, h3 {
  @apply mb-4
}
</style>
