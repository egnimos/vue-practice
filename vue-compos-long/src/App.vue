<script>
import {ref} from 'vue';

export default {
  setup() {
    const name = ref("jhon doe");
    const status = ref("active");
    const tasks = ref(["task 1", "task 2", "task 3", "task 4"]);
    const taskField = ref('');

    const toggleStatus = ()=> {
      if (status.value == 'active') {
        status.value = 'pending'
      } else if (status.value == 'pending') {
        status.value = 'inactive';
      } else {
        status.value = 'active';
      }
    };

    const addTheStatus = () => {
      // value should not be empty
      if (taskField.value.trim() !== '') {
        tasks.value.push(taskField.value);
      }
    };

    const deleteTheStatus = (index) => {
      tasks.value.splice(index, 1);
    };

    return {
      name, status, tasks, taskField, 
      toggleStatus, addTheStatus, deleteTheStatus
    }
  }
}
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status == 'active'">You are active</p>
  <p v-else-if="status == 'pending'">Dude you are in a pending state</p>
  <p v-else>You are a inactive</p>

  <!-- form -->
  <form @submit.prevent="addTheStatus()">
    <label for="Task">Add Task</label>
    <input type="text" v-model="taskField" id="task">
    <button type="submit">Submit</button>
  </form>
  <br><br>
  <!-- list of the tasks -->
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span>{{ task }}</span>
      <button v-on:click="deleteTheStatus(index)">X</button>
    </li>
  </ul>

  <br><br>
  <!-- change the status -->
  <button @click="toggleStatus()">Change Status</button>
</template>

<style scoped>
button {
  margin: 5px;
}

label {
  margin: 5px;
}
</style>