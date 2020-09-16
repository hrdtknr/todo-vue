<template>
  <div>
    <form class="newTodoForm">
      <input v-model="newName" placeholder="new name" />
      <input v-model="newTodo" placeholder="new todo" />
      <button v-on:click="createTodo()">新規登録</button>
    </form>
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
      if (!this.newName && !this.newTodo) {
        alert("NameかTodoのどちらかは入力してください");
      } else {
        axios.post("http://localhost:8000/todoList", {
          name: this.newName,
          todo: this.newTodo,
        });
      }
    },
  },
};
</script>
<style scoped>
.insert {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
.newTodoForm {
  background-color: #42b983;
}
</style>
