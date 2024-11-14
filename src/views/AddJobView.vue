<script setup>
import router from "@/router";
import { reactive } from "vue";
import axios from "axios";
import { useToast } from "vue-toastification";

const form = reactive({
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
const handleSubmit = async () => {
  try {
    const response = await axios.post("/api/jobs", form);
    toast.success("Job added successfully");

    router.push("/jobs/" + response.data.id);
  } catch (error) {
    //@todo - show toast
    toast.error("Failed to add job: " + error.message);
    console.error(error);
  }
};
</script>

<template>
  <div class="bg-green-100 py-12">
    <form
      @submit.prevent="handleSubmit"
      class="container grid gap-4 bg-white p-6 rounded-xl border max-w-md m-auto"
    >
      <h1 class="text-lg font-bold text-center bg-slate-50 pt-2">Add Job</h1>
      <div>
        <p class="text-lg font-semibold">Job Type</p>
        <select
          v-model="form.type"
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
          v-model="form.title"
        />
      </div>
      <div>
        <p class="text-lg font-semibold">Description</p>
        <textarea
          required
          name="decription"
          v-model="form.description"
          class="border rounded-md w-full px-3 py-1"
          placeholder="Add any job duties, expectations, requirements, etc"
        />
      </div>
      <div>
        <p class="text-lg font-semibold">Salary</p>
        <select
          v-model="form.salary"
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
          v-model="form.location"
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
          v-model="form.company.name"
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
          v-model="form.company.email"
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
          v-model="form.company.phone"
          placeholder="Company phone number"
          type="text"
          name="phone"
          class="border rounded-md w-full px-3 py-1"
        />
      </div>

      <button
        class="bg-green-500 text-white text-center py-2 mt-4 hover:bg-opacity-85 rounded-full w-full"
      >
        Add Job
      </button>
    </form>
  </div>
</template>
