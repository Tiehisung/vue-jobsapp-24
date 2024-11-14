<script setup>
import Navbar from "./components/Navbar.vue";
import {RouterView} from "vue-router";
</script>

<template>
  <Navbar />
  <RouterView /><!-- Similar to Outlet in react -->
</template>
