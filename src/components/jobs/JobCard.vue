<script setup>
import logo from "@/assets/logo.svg";
import { RouterLink } from "vue-router";
import { defineProps, ref, computed } from "vue";
const props = defineProps({
  job: {
    type: { type: String, default: "Full-Time" },
    title: String,
    description: String,
    location: String,
    salary: Number,
    company: {
      name: String,
      email: String,
      phone: String,
    },
  },
  //   job: Object, //Alternative
});
const showFullDesc = ref(false);
const truncatedDesc = computed(() => {
  let description = props.job.description;
  if (!showFullDesc.value) {
    description =
      +description.length > 90
        ? description.substring(0, 90) + " ..."
        : description.substring(0, 90);
  }

  return description;
});

const toggleFullDesc = () => {
  showFullDesc.value = !showFullDesc.value;
};
</script>

<template>
  <div class="bg-white px-3 py-6 shadow-lg grid gap-2 max-w-80 rounded-md">
    <p class="text-gray-400">{{ job.type||'Remote' }}</p>
    <h1 class="text-lg font-bold mb-2">{{ job.title }}</h1>
    <div>
      <p>
        {{ truncatedDesc }}
      </p>
      <button
        v-if="job.description.length > 90"
        @click="toggleFullDesc"
        class="text-green-500 hover:text-green-600 mb-3"
      >
        {{ showFullDesc ? "Less" : "More" }}
      </button>
    </div>

    <p class="text-green-500">${{ job.salary }}</p>

    <hr class="mb-5" />

    <p class="text-red-700 flex items-center gap-1">
      <i class="pi pi-map-marker"></i> <span>{{ job.location }}</span>
    </p>

    <RouterLink
      :to="'/jobs/' + job.id"
      class="w-full text-center text-white bg-green-500 rounded-md py-1"
    >
      Read More
    </RouterLink>
  </div>
</template>
