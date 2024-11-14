<script>
// Using the options api approach
export default {
  data() {
    return {
      name: "Soskode",
      status: "pending",
      tasks: ["Task one", "Task two", "Task 3"],
      link: "www.google.com",
    };
  },
  methods: {
    toggleStatus() {
      // if (this.status == "active") this.status = "pending";
      // else if (this.status == "pending") this.status = "inactive";
      // else this.status = "active";

      this.status == "active"
        ? (this.status = "pending")
        : this.status == "pending"
        ? (this.status = "inactive")
        : (this.status = "active");
    },
  },
};
</script>

<template>
  <h1>Vue Jobs</h1>

  <p v-if="status == 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>User is inactive</p>

  <h2>Tasks</h2>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>
  <!-- <a v-bind:href="link" >Click for google</a> -->
  <a :href="link">Click for google</a>
  <br />

  <!-- <button v-on:click="toggleStatus">Toggle status</button> -->
  <button @click="toggleStatus">Toggle status</button>
</template>
