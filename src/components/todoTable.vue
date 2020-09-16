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
          <td>{{ todo.name }}</td>
          <td>{{ todo.todo }}</td>
          <td>
            <form>
              <input v-model="updName" placeholder="updName" />
              <input v-model="updTodo" />
              <button v-on:click="updateTest(todo)">更新</button>
            </form>
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
      console.log(todo);
      if (!this.updName && !this.updTodo) {
        axios.put("http://localhost:8000/todoList", {
          id: todo.id,
          name: "karamoji",
          todo: "karamoji",
        });
      } else {
        axios.put("http://localhost:8000/todoList", {
          id: todo.id,
          name: this.updName,
          todo: this.updTodo,
        });
      }
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
