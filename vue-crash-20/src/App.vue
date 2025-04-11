<script>
export default {
  data() {
    return {
      name: "jhon doe",
      link: "https://www.google.com/",
      list: [
        "Task one",
        "Task two",
        "Task three",
        "Task four",
      ],
      status: "pending",
    }
  },
  methods: {
    toggleStatus() {
      if (this.status == 'active') {
        this.status = 'pending';
      } else if (this.status == 'pending') {
        this.status = 'inactive';
      } else {
        this.status = 'active';
      }
    },

    changeName() {
      this.name = "Welcome!! Niteesh"
    }
  }
}
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status=='active'">Hello we are active</p>
  <p v-else-if="status=='pending'">Yoo! you have somework pending</p>
  <p v-else> You are inactive dude!!</p>

  <h2>List of all the tasks</h2>
  <ol>
    <li v-for="task of list" :key="task">{{ task }}</li>
  </ol>
  <br>
  <a :href="link">Go to Google</a>
  <br>
  <hr>
  <br>
  <button v-on:click="toggleStatus">{{ status }}</button>
  <br>
  <br>
  <button @click="changeName">change name</button>
</template>

<style scoped>
 h1 {
  color: white;
 }
</style>