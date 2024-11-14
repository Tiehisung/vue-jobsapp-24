<script setup>
import { defineProps } from "vue";
defineProps({
  bg: { type: String, default: "bg-gray-100" },
});
</script>

<template>
  <div :class="`grid gap-3 rounded-xl p-4 w-full grow shadow-md ${bg}`">
    <slot></slot>
  </div>
</template>
