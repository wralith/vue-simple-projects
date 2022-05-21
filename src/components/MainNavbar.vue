<script setup lang="ts">
import { RouterLink } from 'vue-router'
</script>

<template>
  <nav>
    <RouterLink to="/">Home</RouterLink>
    <RouterLink to="/about">About</RouterLink>
    <RouterLink to="/todo">Todo List</RouterLink>
  </nav>
</template>

<style>
nav {
  display: flex;
  flex-direction: row;
  justify-content: center;
  gap: 1rem;
}
</style>
