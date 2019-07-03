<template>
  <div>
    <div id="bouton">
      <button @click="eraseTodos">I'm done!</button>
    </div>

    <hr>
    <p v-if="!showText">Enter a new todo here :</p>
    <BaseInputText
      v-if="!showText"
      v-model="newTodoText"
      placeholder="New todo"
      @keydown.enter="addTodo"
    />

    <p v-if="showText">You have completed your todo for the day ! Have a rest</p>

    <ul v-else-if="todos.length">
      <TodoListItem v-for="todo in todos" :key="todo.id" :todo="todo" @remove="removeTodo"/>
    </ul>

    <p v-else>Nothing left in the list. Add a new todo in the input above.</p>
  </div>
</template>

<script>
import BaseInputText from "./BaseInputText.vue";
import TodoListItem from "./TodoListItem.vue";

let nextTodoId = 1;

export default {
  components: {
    BaseInputText,
    TodoListItem
  },
  data() {
    return {
      newTodoText: "",
      showText: false,
      todos: [
        {
          id: nextTodoId++,
          text: "Learn Vue"
        },
        {
          id: nextTodoId++,
          text: "Learn about single-file components"
        },
        {
          id: nextTodoId++,
          text: "My custom todo"
        },
        {
          id: nextTodoId++,
          text: "Fall in love"
        }
      ]
    };
  },
  methods: {
    addTodo() {
      const trimmedText = this.newTodoText.trim();
      if (trimmedText) {
        this.todos.push({
          id: nextTodoId++,
          text: trimmedText
        });
        this.newTodoText = "";
      }
    },
    eraseTodos() {
      this.showText = !this.showText;
    },
    removeTodo(idToRemove) {
      this.todos = this.todos.filter(todo => {
        return todo.id !== idToRemove;
      });
    }
  }
};
</script>

<style scoped>
button {
  background-color: lavenderblush;
  color: purple;
  font-family: "Courier New", Courier, monospace;
  text-align: center;
}
#bouton {
  text-align: center;
}
</style>
