<script setup>
import { defineProps } from "vue";
defineProps({
  title: {
    type: String,
    default: "Become a Vue Developer",
  },
  subtitle: {
    type: String,
    default: "Find the job that fits your skills and needs",
  },
});
</script>

<template>
  <div class="bg-green-500 text-white font-bold p-6 text-center border-t">
    <h1 class="text-xl">{{ title }}</h1>
    <p class="font-light">{{ subtitle }}</p>
  </div>
</template>
