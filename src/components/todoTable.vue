<template>
  <div>
    <table class="table">
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
        <tr v-for="todo in todoList" :key="todo.id">
          <td>{{ todo.id }}</td>
          <td>{{ todo.name }}</td>
          <td>{{ todo.todo }}</td>
          <td>
            <form>
              <input v-model="updName" />
              <input v-model="updTodo" />
              <button v-on:click="updateTest(todo)" />
            </form>
          </td>
          <td>
            <button v-on:click="deleteTest(todo.id)" />
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
    axios
      .get("http://localhost:8000/todoList")
      .then((response) => (this.todoList = response.data))
      .catch((error) => console.log(error));
  },
  methods: {
    updateTest: function(todo) {
      axios.put("http://localhost:8000/todoList", {
        id: todo.id,
        name: this.updName + "update",
        todo: this.updTodo + "update",
      });
    },
    deleteTest: function(delId) {
      console.log("delete:", delId); // test
      axios.delete("http://localhost:8000/todoList", {
        id: delId,
      });
    },
  },
};
</script>
