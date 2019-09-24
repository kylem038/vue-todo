<template>
  <div>
    <h1>Todo List</h1>
    <input type="text" v-model="inputText" />
    <button @click="submitTodo">Add Todo</button>
    <ol>
      <li class="todo" v-for="(duck, index) in todos" :key="index">
        <input
          type="checkbox"
          v-model="duck.done"
          true-value="true"
          false-value="false"
        />
        {{ duck.name }} <button @click="removeTodo(index)">Delete</button>
        <button @click="moveUp(duck, index)">Move up</button>
      </li>
    </ol>
  </div>
</template>

<script>
export default {
  name: "Todo",
  data() {
    return {
      inputText: "",
      todos: []
    };
  },
  methods: {
    submitTodo() {
      this.todos.push({ name: this.inputText, done: false });
      this.inputText = "";
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    moveUp(duck, index) {
      if (index === 0) {
        return;
      }
      this.todos.splice(index, 1);

      this.todos.splice(index - 1, 0, duck);
    }
  }
};
</script>

<style scope>
.todo {
  text-align: left;
}
</style>
