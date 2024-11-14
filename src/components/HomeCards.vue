<script setup>
import {RouterLink}from 'vue-router'
import Card from "./Card.vue";
</script>

<template>
  <!-- for developers -->
  <div class="flex flex-wrap sm:flex-nowrap my-5 gap-6 container m-auto">
    <Card>
      <h1 class="font-extrabold text-xl">For Developers</h1>
      <p>Browse our Vue jobs and start your career</p>
      <RouterLink to="/jobs"
        class="bg-black text-white px-3 py-2 rounded-md text-center w-fit"
      >
        Browse Jobs
      </RouterLink>
    </Card>

    <Card bg="bg-green-100">
      <h1 class="font-extrabold text-xl">For Employers</h1>
      <p>List your Job to find the perfect developer for the role</p>
      <RouterLink
      to="/jobs/add"
        class="bg-green-500 text-white px-3 py-2 rounded-md text-center w-fit"
      >
        Add Job
      </RouterLink>
    </Card>
  </div>
</template>
