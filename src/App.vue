<script setup lang="ts">
import { RouterView } from 'vue-router'
import MainNavbar from './components/MainNavbar.vue'
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <p>Hello, I am Wralith</p>
    </div>
    <MainNavbar />
    <hr />
  </header>

  <RouterView />
</template>

<style lang="scss">
header {
  align-items: center;
  text-align: center;
}

hr {
  border-color: rgba(128, 128, 128, 0.562);
}
</style>
