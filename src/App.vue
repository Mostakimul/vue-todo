<script setup>
import { RouterView } from 'vue-router';
import TodoNavigation from './components/TodoNavigation.vue';
</script>

<template>
  <main class="container mx-auto">
    <TodoNavigation />
    <RouterView />
  </main>
</template>

<style></style>
