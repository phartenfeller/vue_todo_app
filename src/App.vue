<template>
  <div id="app">
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet" />
    <h1>Todo-List</h1>
    <div>
      <div>Total Todos: {{todos.length}}</div>
      <m-text-field outlined id="todo-input" class="todo-input" v-model="inputText">
        <m-floating-label for="todo-input">New Todo</m-floating-label>
      </m-text-field>
      <m-button raised v-on:click="addTodo" class="add-button">Add</m-button>
    </div>
    <TodoList :todos="todos" v-on:removeTodo="removeTodo" />
  </div>
</template>

<script>
import Vue from "vue";
import TodoList from "./components/TodoList.vue";

import Button from "material-components-vue/dist/button";
import TextField from "material-components-vue/dist/text-field";
import FloatingLabel from "material-components-vue/dist/floating-label";
import Checkbox from "material-components-vue/dist/checkbox";
import IconButton from "material-components-vue/dist/icon-button";
import Icon from "material-components-vue/dist/icon";

Vue.use(Button);
Vue.use(TextField);
Vue.use(FloatingLabel);
Vue.use(Checkbox);
Vue.use(IconButton);
Vue.use(Icon);

export default {
  name: "app",
  components: {
    TodoList
  },
  data: () => {
    return {
      id: 0,
      todos: [{ id: 0, text: "Vue testen", done: false }],
      inputText: ""
    };
  },
  methods: {
    addTodo: function() {
      if (this.inputText !== "") {
        this.id += 1;
        this.todos.push({
          id: this.id,
          text: this.inputText,
          done: false
        });
        this.inputText = "";
      }
    },
    removeTodo: function(removeId) {
      const index = this.todos.findIndex(todo => (todo.id = removeId));
      this.todos.splice(index, 1);
    }
  }
};
</script>

<style lang="scss">
$main-green: #42b983;

@import "material-components-vue/dist/button/styles.scss";
@import "material-components-vue/dist/text-field/styles.scss";
@import "material-components-vue/dist/floating-label/styles.scss";
@import "material-components-vue/dist/checkbox/styles.scss";
@import "material-components-vue/dist/icon-button/styles.scss";

.todo-input {
  @include mdc-text-field-label-color($main-green);
  @include mdc-text-field-focused-outline-color($main-green);
  @include mdc-text-field-outline-color(#000);
}

.add-button {
  @include mdc-button-filled-accessible($main-green);

  margin: 10px;
}

.chk {
  @include mdc-checkbox-container-colors(
    $marked-stroke-color: $main-green,
    $marked-fill-color: $main-green
  );
}

.material-icons {
  font-family: "Material Icons";
  font-weight: normal;
  font-style: normal;
  font-size: 24px; /* Preferred icon size */
  display: inline-block;
  line-height: 1;
  text-transform: none;
  letter-spacing: normal;
  word-wrap: normal;
  white-space: nowrap;
  direction: ltr;

  /* Support for all WebKit browsers. */
  -webkit-font-smoothing: antialiased;
  /* Support for Safari and Chrome. */
  text-rendering: optimizeLegibility;

  /* Support for Firefox. */
  -moz-osx-font-smoothing: grayscale;

  /* Support for IE. */
  font-feature-settings: "liga";
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
h1 {
  margin: 40px 0 0;
  color: $main-green;
}
</style>
