<script setup>
import { RouterLink } from "vue-router";
</script>

<template>
  <div
    class="flex flex-col justify-center items-center border p-12 rounded-2xl"
  >
    <p class="text-3xl font-semibold text-neutral-700 my-6">
      <i class="pi pi-exclamation-triangle"></i>
      Sorry! Page not found
    </p>

    <RouterLink
      to="/"
      class="text-red-400 bg-red-100 rounded shadow-md px-3 py-1 transform duration-150"
    >
      Return to home page</RouterLink
    >
  </div>
</template>
