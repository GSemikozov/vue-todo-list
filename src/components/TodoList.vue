<template>
  <div class='card'>
    <h3>Your tasks</h3>
    <p class='tasks'>Done: <b class="text-success">{{todos.filter(todo => {return todo.done === true}).length}}</b> / Not done: <b style="color: red">{{todos.filter(todo => {return todo.done === false}).length}}</b> task(s)</p>
    <todo v-for="todo in todos"
          v-on:delete-todo="deleteTodo"
          v-on:complete-todo="completeTodo"
          v-on:save-todo="saveTodo"
          v-bind:key="todo.id"
          :todo.sync="todo">
    </todo>
  </div>
</template>
<script type="text/javascript">
import Todo from './Todo'
import todoStorage from './TodoStorage'
export default {
  props: ['todo', 'todos'],
  components: {
    Todo
  },
  methods: {
    deleteTodo (todo) {
      const todoIndex = this.todos.indexOf(todo)
      this.todos.splice(todoIndex, 1)
      todoStorage.deleteItem(todo)
    },
    completeTodo (todo) {
      const todoIndex = this.todos.indexOf(todo)
      this.todos[todoIndex].done = true
      todoStorage.save(this.todos)
    },
    saveTodo () {
      todoStorage.save(this.todos)
    }
  }
}
</script>

<style scoped>
.card h3, .card p {
  padding: 0 25px;
}
.tasks {
  font-size: .9em;
  color: #afafaf;
}
.card {
  border-radius: 0;
  border-top: none;
  z-index: 1;
  padding: 40px 0 0;
}
</style>

