<script setup>
import { ref, onMounted } from 'vue';

const name = ref('Niteesh');
const status = ref('active');
const tasks = ref([]);
const taskField = ref('');

function toggleStatus() {
  if (status.value == 'active') {
    status.value = 'pending';
  } else if (status.value == 'pending') {
    status.value = 'inactive';
  } else {
    status.value = 'active';
  }
}

function addTask() {
  if (taskField.value.trim() !== '') {
    tasks.value.push(taskField.value)
  }
}

const deleteTask = (i) => {
  tasks.value.splice(i, 1)
}

onMounted(async () => {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/todos");
    const tasksData = await response.json()
    tasks.value = tasksData.map((task) => task.title)
  } catch (error) {
    console.log("Error: ", error);
  }
});

</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status == 'active'">you are a active user</p>
  <p v-else-if="status == 'pending'">you are in a pending state</p>
  <p v-else>dude you are a inactive</p>

  <br>

  <form @submit.prevent="addTask">
    <label for="Task">Add Task</label>
    <input type="text" id="task" v-model="taskField">
    <button type="submit">Submit</button>
  </form>

  <br>

  <ol>
    <li v-for="(task, i) in tasks" :key="task">
      <span>{{ task }}</span>
      <button type="button" @click="deleteTask">X</button>
    </li>
  </ol>

  <br>

  <button type="button" v-on:click="toggleStatus">change status</button>
</template>

<style scoped>
button,
label {
  margin: 5px;
}
</style>