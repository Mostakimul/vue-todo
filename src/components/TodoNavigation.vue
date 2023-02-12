<template>
  <header>
    <nav
      class="bg-gray-300 rounded-md mt-5 p-5 flex justify-between items-center"
    >
      <div class="flex items-center gap-2">
        <img src="../assets/vue_logo.png" alt="vue-logo" class="w-16" />
        <h2 class="font-bold">Vue Todos</h2>
      </div>
      <ul class="font-bold flex gap-3">
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </ul>
    </nav>
  </header>
</template>

<script setup></script>
