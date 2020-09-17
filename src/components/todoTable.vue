<template>
  <div>
    <table class="table" border="3">
      <thead>
        <tr>
          <th>ID</th>
          <th>NAME</th>
          <th>TODO</th>
          <th>EDIT</th>
          <th>DELETE</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="todo in todoList" v-bind:key="todo.id">
          <td>{{ todo.id }}</td>
          <td>
            <input
              type="text"
              v-model="todo.name"
              v-on:keyup.enter="(isUpdName = false), updateTodo(todo)"
            />
          </td>
          <td>
            <input
              type="text"
              v-model="todo.todo"
              v-on:keyup.enter="(isUpdTodo = false), updateTodo(todo)"
              v-bind:key="todo.id"
            />
          </td>
          <td>
            <button v-on:click="updateTodo(todo)">更新</button>
          </td>
          <td>
            <button v-on:click="deleteTodo(todo.id)">削除</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      todoList: null,
      updName: "",
      updTodo: "",
      isUpdName: false,
      isUpdTodo: false,
      borderColor: "black",
    };
  },
  mounted() {
    axios
      .get("http://localhost:8000/todoList")
      .then((response) => (this.todoList = response.data))
      .catch((error) => console.log(error));
  },
  methods: {
    getTodo: function() {
      axios
        .get("http://localhost:8000/todoList")
        .then((response) => (this.todoList = response.data))
        .catch((error) => console.log(error));
    },
    updateTodo: function(todo) {
      axios.put("http://localhost:8000/todoList", {
        id: todo.id,
        name: todo.name,
        todo: todo.todo,
      });
    },
    deleteTodo: function(delId) {
      const params = { id: delId };
      const qs = new URLSearchParams(params);
      axios
        .delete(`http://localhost:8000/todoList?${qs}`)
        .then(() => this.getTodo());
    },
    setBorderColor: function(color) {
      this.borderColor = color;
    },
  },
};
</script>
<style scoped>
.table {
  background-color: aqua;
}
</style>
