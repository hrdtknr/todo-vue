<template>
  <div>
    <table class="table">
      <thead>
        <tr>
          <th>ID</th>
          <th>NAME</th>
          <th>TODO</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="todo in todoList" :key="todo.id">
          <td>{{ todo.id }}</td>
          <td>{{ todo.name }}</td>
          <td>{{ todo.todo }}</td>
          <td>
            <button v-on:click="postTest()" />
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
    };
  },
  mounted() {
    axios
      .get("http://localhost:8000/todoList")
      .then(
        (response) => (
          console.log("axios get"),
          console.log(response),
          (this.todoList = response.data)
        )
      )
      .catch((error) => console.log(error));
  },
  methods: {
    test: function() {
      console.log("test function");
    },
    postTest: function() {
      axios.post("http://localhost:8000/todoList", {
        id: 1,
        name: "json name",
        todo: "json todo",
      });
    },
  },
};
</script>
