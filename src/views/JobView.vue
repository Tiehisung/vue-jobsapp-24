<script setup>
import jobsData from "@/data/jobs.json";
import { onMounted, reactive } from "vue";
import PulseLoader from "vue-spinner/src/PulseLoader.vue";
import { useRoute, RouterLink } from "vue-router";
import { useToast } from "vue-toastification";
import router from "@/router";
import axios from "axios";

const route = useRoute();

const jobId = route.params.id;
const state = reactive({ job: {}, isLoading: true, isDeleting: false });

onMounted(async () => {
  try {
    const response = await axios.get(`/api/jobs/` + jobId);
    state.job = response.data;
  } catch (error) {
    console.error(error);
  } finally {
    state.isLoading = false;
  }
});

const toast = useToast();
const handleDelete = async () => {
  try {
    const confirm = window.confirm("Are you sure you want to delete this job?");
    if (!confirm) return;
    state.isDeleting = true;
    const response = await axios.delete("/api/jobs/" + jobId);
    toast.success("Job deleted successfully");
    router.replace("/jobs");
  } catch (error) {
    toast.error("Failed to delete job. " + error.message);
  } finally {
    state.isDeleting = false;
  }
};
</script>

<template>
  <main class="bg-blue-200 min-h-[90vh] px-[5vw] py-8">
    <div v-if="state.isLoading" class=""><PulseLoader /></div>
    <div class="grid md:grid-cols-7/3 gap-6 container m-auto">
      <section class="space-y-5">
        <div class="p-4 pb-8 rounded-md bg-white grid gap-4">
          <p class="text-gray-400 font-light">{{ state.job.type }}</p>

          <h1 class="font-bold text-xl">{{ state.job.title }}</h1>

          <p>{{ state.job.location }}</p>
        </div>
        <div class="p-4 pb-8 rounded-md bg-white grid gap-4">
          <p class="text-green-700 font-semibold">Job Description</p>

          <h1 class="font-bold text-xl">{{ state.job.description }}</h1>

          <div>
            <p class="text-green-700 font-semibold">Salary</p>
            <p>${{ state.job.salary }}</p>
          </div>
        </div>
      </section>

      <section class="space-y-6">
        <div class="bg-white rounded-md p-4 grid gap-3 w-full">
          <h1 class="font-bold text-xl">Company Info</h1>

          <h3 class="text-lg font-semibold mt-7">
            {{ state.job.company?.name }}
          </h3>
          <p>
            Lorem ipsum dolor sit, amet consectetur adipisicing elit. Rem
            corporis vero quidem? Voluptatibus aspernatur expedita, sunt cumque
            recusandae veritatis? Ab. Lorem ipsum dolor sit, amet consectetur
            adipisicing elit. Rem corporis vero quidem? Voluptatibus aspernatur
            expedita, sunt cumque recusandae veritatis? Ab. Lorem ipsum d
          </p>

          <div class="mt-7">
            <h4>Contact Email</h4>
            <p class="text-green-800 bg-green-300 font-bold px-2 py-1 rounded">
              {{ state.job.company?.email }}
            </p>
          </div>

          <div class="mt-2">
            <h4>Contact Email</h4>
            <p class="text-green-800 bg-green-300 font-bold px-2 py-1 rounded">
              {{ state.job.company?.phone }}
            </p>
          </div>
        </div>

        <!-- Actions -->

        <div class="grid gap-3 rounded-md bg-white p-4 w-full">
          <h2 class="font-bold mb-2">Manage Job</h2>
          <RouterLink
            :to="`/jobs/edit/${jobId}`"
            class="bg-green-500 text-white text-center py-1 hover:bg-opacity-85 rounded-full w-full"
            >Edit Job</RouterLink
          >
          <button
            @click="handleDelete"
            class="bg-red-500 text-white text-center py-1 hover:bg-opacity-85 rounded-full w-full"
          >
            <PulseLoader v-if="state.isDeleting" />
            {{ state.isDeleting ? "Deleting " : "Delete " }} Job
          </button>
        </div>
      </section>
    </div>
  </main>
</template>
