<template>
  <div>
    <v-card-actions>
      <v-btn @click="sendRequest()">test</v-btn>
    </v-card-actions>
    <table class="table">
      <thead>
        <tr>
          <th>ID</th>
          <th>NAME</th>
          <th>TODO</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="todo in todoList" :key="todo.id">
          <td>{{ todo.id }}</td>
          <td>{{ todo.name }}</td>
          <td>{{ todo.todo }}</td>
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
      .then((response) => (this.todoList = response.data))
      .catch((error) => console.log(error));
  },
  methods: {
    sendRequest: function() {
      axios.post("http://localhost:8000/todoList", {
        id: 1,
        name: "json name",
        todo: "json todo",
      });
    },
  },
};
</script>
