<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <nav class="mx-5">
        <RouterLink to="/" class="btn-one">Home</RouterLink>
        <RouterLink to="/about" class="btn-one">About</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 12px 0px 12px 0px;
}
.logo {
  width: 70px;
}
nav {
  display: flex;
  gap: 20px;
  align-self: center;
}

@media (min-width: 1024px) {
}
</style>
