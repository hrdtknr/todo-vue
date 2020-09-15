<template>
  <div>
    {{ data }}
    <table border>
      <tr>
        <th>県名</th>
        <th>県庁所在地</th>
      </tr>
      <tr>
        <td>茨城県</td>
        <td>水戸市</td>
      </tr>
      <tr>
        <td>栃木県</td>
        <td>宇都宮市</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      data: "",
    };
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
