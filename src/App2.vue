<!-- Options API -->

<script>
export default {
  data() {
    return {
      name: 'John Doe',
      status: 'active',
      tasks: ['task1', 'task2', 'task3'],
      link: 'https://www.google.com',
    };
  },
  methods: {
    toggleStatus() {
      if (this.status === 'active') {
        this.status = 'pending';
      } else if (this.status === 'pending') {
        this.status = 'inactive';
      } else {
        this.status = 'active';
      }
    },
  },
};
</script>

<template>
  <div class="parent">
    <h1>{{ name }}</h1>
    <p v-if="status === 'active'">User is active</p>
    <p v-else-if="status === 'inactive'">User is inactive</p>
    <p v-else>User is pending</p>
    <h3>Tasks</h3>
    <ul>
      <li v-for="task in tasks" :key="task">{{ task }}</li>
    </ul>
    <!-- <a v-bind:href="link">Click for Google</a> -->
    <a :href="link">Click for Google</a>
    <!-- <button v-on:click="toggleStatus">Change Status</button> -->
    <button @click="toggleStatus">Change Status</button>
  </div>
</template>

<style scoped>
.parent {
  display: flex;
  flex-direction: column;
}
h1 {
  color: black;
}
</style>
