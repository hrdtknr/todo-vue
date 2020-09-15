<template>
  <div class="divTable">
    <myheader></myheader>
    <p v-if="msg.length > 0">{{ msg[0].id }}</p>
    <p v-else>no text</p>
    <input type="text" v-model="msg[0].name" />
    <button @click="clear()">clear</button>
  </div>
</template>

<script>
import myheader from "./components/myheader";

export default {
  components: {
    myheader,
  },
  data() {
    return {
      msg: "Hello World!",
    };
  },
  methods: {
    clear() {
      this.msg = "";
    },
  },
  created() {
    fetch("http://localhost:8000/todoList/data")
      .then((response) => {
        return response.json();
      })
      .then((json) => {
        console.log(json);
        this.msg = json;
      })
      .catch((err) => {
        this.msg = err; // エラー処理
      });
  },
};
</script>
