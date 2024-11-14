<script setup>
import { ref, onMounted } from "vue";

// By the composition api approach

const name = ref("Soskode");
const status = ref("active");
const newTask = ref("");
const tasks = ref(["Task one", "Task two", "Task 3"]);
const handleToggleStatus = () => {
  if (status.value == "active") status.value = "pending";
  else if (status.value == "pending") status.value = "inactive";
  else status.value = "active";
};

const addTask = () => {
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value);
    newTask.value = "";
  }
};
const removeTask = (index) => {
  tasks.value = tasks.value.filter((t, i) => i !== index);
};

//Fetch from jsonplaceholder
onMounted(async () => {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/todos");
    const result = await response.json();
    tasks.value = result.map((r) => r.title);
  } catch (error) {
    console.log({ error });
  }
});
</script>

<template>
  <h1>Vue Jobs</h1>

  <p v-if="status == 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>User is inactive</p>
  <!-- Form -->
  <form v-on:submit.prevent="addTask">
    <input type="text" v-model="newTask" />
    <button type="submit">Submit</button>
  </form>
  <h2>Tasks</h2>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span>{{ task }}</span
      ><button @click="removeTask(index)">x</button>
    </li>
  </ul>

  <br />

  <button @click="handleToggleStatus">Toggle status</button>
</template>
