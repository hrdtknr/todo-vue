<template>
  <div>
    <table class="table" border="3">
      <thead>
        <tr>
          <th>ID</th>
          <th>NAME</th>
          <th>TODO</th>
          <th>DELETE</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="todo in todoList" :key="todo.id">
          <td>{{ todo.id }}</td>
          <td>{{ todo.name }}</td>

          <td v-if="!isUpdTodo" v-on:dblclick="isUpdTodo = true">
            {{ todo.todo }}
          </td>
          <td v-else>
            <input
              type="text"
              v-model="todo.todo"
              v-on:keyup.enter="updateTest(todo)"
            />
          </td>
          <td>
            <button v-on:click="deleteTest(todo.id)">削除</button>
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
    };
  },
  mounted() {
    //ここのデータを再取得かな_関数へ移動？
    axios
      .get("http://localhost:8000/todoList")
      .then((response) => (this.todoList = response.data))
      .catch((error) => console.log(error));
  },
  methods: {
    getTest: function() {
      axios
        .get("http://localhost:8000/todoList")
        .then((response) => (this.todoList = response.data))
        .then(() => this.getTest())
        .catch((error) => console.log(error));
    },
    updateTest: function(todo) {
      axios
        .put("http://localhost:8000/todoList", {
          id: todo.id,
          name: todo.name,
          todo: todo.todo,
        })
        .then(() => this.getTest());
    },
    deleteTest: function(delId) {
      const params = { id: delId };
      const qs = new URLSearchParams(params);
      axios
        .delete(`http://localhost:8000/todoList?${qs}`)
        .then(() => this.getTest());
    },
  },
};
</script>
<style scoped>
.table {
  background-color: aqua;
  border: 1;
}
</style>
