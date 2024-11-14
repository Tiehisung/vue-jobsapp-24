<script setup>
import { RouterLink } from "vue-router";
import JobCard from "./JobCard.vue";
import { reactive, defineProps, onMounted } from "vue"; //For responsive
import axios from "axios";
import PulseLoader from "vue-spinner/src/PulseLoader.vue";
defineProps({
  limit: Number,
  showButton: { type: Boolean, default: false },
  styles: String,
});
const state = reactive({ jobs: [], waiting: true });

onMounted(async () => {
  try {
    const response = await axios.get("/api/jobs");
    state.jobs = response.data;

    console.log({ response });
  } catch (error) {
    console.error(error);
  } finally {
    state.waiting = false;
  }
});
</script>

<template>
  <div :class="` bg-green-100 p-3 ${styles} `">
    <h1 class="w-full my-3 px-3 text-center text-2xl text-green-500 font-bold">
      Browse Jobs
    </h1>

    <div
      v-if="state.waiting"
      class="text-red-500 flex items-center justify-center p-10 w-full"
    >
      <PulseLoader />
    </div>

    <ul
      v-else
      class="grid gap-6 container m-auto md:grid-cols-2 xl:grid-cols-3 2xl:grid-cols-4"
    >
      <li
        v-for="job of state.jobs.slice(0, limit || state.jobs.length)"
        :key="job.id"
      >
        <JobCard :job="job" />
      </li>
    </ul>

    <div v-if="showButton" class="flex items-center justify-center">
      <RouterLink
        to="/jobs"
        class="bg-gray-200 text-gray-800 text-sm border rounded-full px-4 py-1"
      >
        View all</RouterLink
      >
    </div>
  </div>
</template>
