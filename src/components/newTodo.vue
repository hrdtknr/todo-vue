<template>
  <div>
    <form class="newTodoForm">
      <input v-model="newName" placeholder="new name" />
      <input v-model="newTodo" placeholder="new todo" />
      <button v-on:click="createTodo()" />
    </form>
    <p>new name is {{ newName }}</p>
    <p>new todo is {{ newTodo }}</p>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      newName: "",
      newTodo: "",
    };
  },
  methods: {
    createTodo: function() {
      // ok
      console.log("uanirweganiug");
      axios.post("http://localhost:8000/todoList", {
        name: this.newName,
        todo: this.newTodo,
      });
    },
  },
};
</script>
