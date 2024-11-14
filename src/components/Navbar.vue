<script setup>
import { RouterLink, useRoute } from "vue-router";
import logo from "@/assets/logo.svg";

const isActive = (path) => {
  const route = useRoute();
  return route.path === path;
};
</script>

<template>
  <nav class="flex items-center gap-3 justify-center bg-green-500 py-2">
    <div class="w-28 flex items-center justify-end">
      <img :src="logo" alt="logo" class="h-12 w-12 rounded-full" />
    </div>

    <div class="flex gap-4 items-center justify-center grow text-white">
      <RouterLink
        to="/"
        :class="`hover:bg-gray-500/30 p-2 rounded transition-all duration-150 delay-75 ease-linear ${isActive('/')?'bg-gray-300/50':''}`"
        >Home</RouterLink
      >
      <RouterLink
        to="/jobs"
        :class="`hover:bg-gray-500/30 p-2 rounded transition-all duration-150 delay-75 ease-linear ${isActive('/jobs')?'bg-gray-300/50':''}`"
        >Jobs</RouterLink
      >
      <RouterLink
        to="/jobs/add"
        :class="`hover:bg-gray-500/30 p-2 rounded transition-all duration-150 delay-75 ease-linear ${isActive('/jobs/add')?'bg-gray-300/50':''}`"
        >Add Job</RouterLink
      >
    </div>
  </nav>
</template>
