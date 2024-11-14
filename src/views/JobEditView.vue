<script setup>
import router from "@/router";
import { reactive, onMounted } from "vue";
import { useToast } from "vue-toastification";
import { useRoute } from "vue-router";
import PulseLoader from "vue-spinner/src/PulseLoader.vue";
import axios from "axios";

const route = useRoute();
const jobId = route.params.id;

const state = reactive({
  job: {
    type: "Full-Time",
    title: "",
    description: "",
    location: "",
    salary: "",
    company: {
      name: "",
      email: "",
      phone: "",
    },
  },
  isUpdating: false,
  isFetching: true,
});

const salaryRanges = [
  "12-17k/year",
  "20-30k/year",
  "30-50k/year",
  "50-100k/year",
  "100-150k/year",
  "150-200k/year",
  "200-230k/year",
  "230-270k/year",
  "270-300k/year",
];

//Init toastification
const toast = useToast();
const handleUpdate = async () => {
  state.isUpdating = true;
  try {
    setTimeout(async () => {
      const response = await axios.put("/api/jobs/" + jobId, state.job);
      toast.success("Job added successfully");
      router.push("/jobs/" + jobId);
    }, 1000);
  } catch (error) {
    toast.error("Failed to add job: " + error.message);
    console.error(error);
  } finally {
    state.isUpdating = false;
  }
};

//mount

onMounted(async () => {
  try {
    const response = await axios.get("/api/jobs/" + jobId);
    state.job = response.data;
  } catch (error) {
    toast.error("Failed to fetch");
  } finally {
    state.isFetching = false;
  }
});
</script>

<template>
  <div class="bg-green-100 py-12">
    <div v-if="state.isFetching">
      <PulseLoader />
    </div>
    <form
      v-else="state.isFetching"
      @submit.prevent="handleUpdate"
      class="container grid gap-4 bg-white p-6 rounded-xl border max-w-md m-auto"
    >
      <h1 class="text-lg font-bold text-center bg-slate-50 pt-2">
        Edit - {{ state.job.title }}
      </h1>
      <div>
        <p class="text-lg font-semibold">Job Type</p>
        <select
          v-model="state.job.type"
          name="type"
          class="border rounded-md w-full px-3 py-1"
          required
        >
          <option value="">Select Job type</option>
          <option value="Full-Time">Full-Time</option>
          <option value="Part-Time">Part-Time</option>
          <option value="Remote">Remote</option>
        </select>
      </div>
      <div>
        <p class="text-lg font-semibold">Job Listing Title</p>
        <input
          required
          placeholder="eg. Software Engineer"
          type="text"
          name="title"
          class="border rounded-md w-full px-3 py-1"
          v-model="state.job.title"
        />
      </div>
      <div>
        <p class="text-lg font-semibold">Description</p>
        <textarea
          required
          name="decription"
          v-model="state.job.description"
          class="border rounded-md w-full px-3 py-1"
          placeholder="Add any job duties, expectations, requirements, etc"
        />
      </div>
      <div>
        <p class="text-lg font-semibold">Salary</p>
        <select
          v-model="state.job.salary"
          required
          name="salary"
          id="salary"
          class="border rounded-md w-full px-3 py-1"
        >
          <option value="">Select range</option>
          <option v-for="sr of salaryRanges" :key="sr" :value="sr">
            {{ sr }}
          </option>
        </select>
      </div>
      <div>
        <p class="text-lg font-semibold">Location</p>
        <input
          required
          v-model="state.job.location"
          placeholder="Company location"
          type="text"
          name="location"
          class="border rounded-md w-full px-3 py-1"
        />
      </div>

      <h2 class="text-lg font-semibold text-gray-700">Company information</h2>
      <div>
        <p class="text-lg font-semibold">Name</p>
        <input
          required
          v-model="state.job.company.name"
          placeholder="Company name"
          type="text"
          name="company"
          class="border rounded-md w-full px-3 py-1"
        />
      </div>
      <div>
        <p class="text-lg font-semibold">Email</p>
        <input
          required
          v-model="state.job.company.email"
          placeholder="Company email"
          type="email"
          name="email"
          class="border rounded-md w-full px-3 py-1"
        />
      </div>
      <div>
        <p class="text-lg font-semibold">Phone</p>
        <input
          required
          v-model="state.job.company.phone"
          placeholder="Company phone number"
          type="text"
          name="phone"
          class="border rounded-md w-full px-3 py-1"
        />
      </div>

      <button
        @click="handleUpdate"
        class="flex items-center justify-center gap-2 bg-teal-500 text-white text-center py-2 mt-4 hover:bg-opacity-85 rounded-full w-full"
      >
        {{ state.isUpdating ? "Saving... " : "Save changes" }}

        <div v-if="state.isUpdating">
          <PulseLoader />
        </div>
      </button>
    </form>
  </div>
</template>
