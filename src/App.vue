<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <div class="m-4">
    <header class="mb-4">
        <nav class="flex gap-4">
          <RouterLink class="border rounded bg-gray-100 px-3 py-1.5" to="/">Home</RouterLink>
          <RouterLink class="border rounded bg-gray-100 px-3 py-1.5" to="/about">About</RouterLink>
        </nav>
    </header>

    <RouterView />
  </div>

</template>

