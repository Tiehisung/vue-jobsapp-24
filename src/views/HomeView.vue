<script setup>
import Hero from "@/components/Hero.vue";
import HomeCards from "@/components/HomeCards.vue";
import BrowseJobs from "@/components/jobs/Browse.vue";
</script>

<template>
  <Hero title="Become a better Vue engineer" />
  <HomeCards />
  <BrowseJobs :limit="4" showButton />
</template>
