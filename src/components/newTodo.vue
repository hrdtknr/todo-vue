<template>
  <div>
    <form class="newTodoForm">
      <input type="text" id="newName" placeholder="Name" />
      <input type="text" id="newTodo" placeholder="Todo" />
      <input type="button" onclick="createTodo()" value="新規TODO追加" />
    </form>
  </div>
</template>
<script>
createTodo();
function createTodo() {
  console.log("newtodo");
}
</script>
