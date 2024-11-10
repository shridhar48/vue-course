<!-- Composition API -->

<script setup>
import { ref, onMounted } from 'vue';

const name = ref('John Doe');
const status = ref('active');
const tasks = ref(['task1', 'task2', 'task3']);
const newTask = ref('');

const toggleStatus = () => {
  if (status.value === 'active') {
    status.value = 'pending';
  } else if (status.value === 'pending') {
    status.value = 'inactive';
  } else {
    status.value = 'active';
  }
};

const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value);
    newTask.value = '';
  }
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

onMounted(async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos');
    const data = await response.json();
    tasks.value = data.map((task) => task.title);
  } catch (error) {
    console.error('Error fetching tasks');
  }
});
</script>

<template>
  <div class="parent">
    <h1>{{ name }}</h1>
    <p v-if="status === 'active'">User is active</p>
    <p v-else-if="status === 'inactive'">User is inactive</p>
    <p v-else>User is pending</p>
    <form @submit.prevent="addTask">
      <label for="newtasks">Add task</label>
      <input type="text" id="newTask" name="newTask" v-model="newTask" />
      <button type="submit">Submit</button>
    </form>
    <h3>Tasks</h3>
    <ul>
      <li v-for="(task, index) in tasks" :key="task">
        <span>{{ task }}</span
        ><button @click="deleteTask(index)">x</button>
      </li>
    </ul>
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
