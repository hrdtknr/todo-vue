<template>
  <div class="divTable">
    <newTodo></newTodo>
    <todoTable></todoTable>
  </div>
</template>

<script>
import todoTable from "./components/todoTable";
import newTodo from "./components/newTodo";
export default {
  components: {
    todoTable,
    newTodo,
  },
  data() {
    return {
      msg: "",
      data: "",
    };
  },
  methods: {
    clear() {
      this.msg = "";
    },
  },
  created() {
    fetch("http://localhost:8000/todoList")
      .then((response) => {
        return response.json();
      })
      .then((json) => {
        this.data = json;
      })
      .catch((err) => {
        this.data = err; // エラー処理
      });
  },
};
</script>
