<template>
  <div class="divTable">
    <myheader></myheader>
    <ul v-for="m in data" :key="m.id">
      {{
        m.id
      }},
      {{
        m.name
      }},
      {{
        m.todo
      }}
    </ul>
    <todoTable></todoTable>
    <Tes msg2="data" />
  </div>
</template>

<script>
import myheader from "./components/myheader";
import todoTable from "./components/todoTable";
import Tes from "./components/Test";
export default {
  components: {
    myheader,
    todoTable,
    Tes,
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
        console.log(json);
        this.data = json;
      })
      .catch((err) => {
        this.data = err; // エラー処理
      });
  },
};
</script>
