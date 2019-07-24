<template>
  <div id="todoList">
    <div v-for="todo in todos" v-bind:key="todo.id" class="todo-item">
      <span>{{ todo.text }}</span>
      <m-checkbox v-model="todo.done" class="chk" />
      <m-icon-button v-on:click="$emit('removeTodo', 'todo.id')">
        <m-icon icon="delete" />
      </m-icon-button>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoList",
  props: {
    todos: {
      type: Array,
      required: true
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.todo-item {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
