<template>
  <div id="app" class="container m-y-3">
    <h1 class="text-center">Test Todo App</h1>
    <div class='row justify-content-md-center'>
      <div class='col-sm-4 col-sm-offset-4'>
        <create-todo v-on:create-todo="createTodo"></create-todo>
        <todo-list v-bind:todos="todos"></todo-list>
      </div>
    </div>
  </div>
</template>

<script>
import TodoList from './components/TodoList'
import CreateTodo from './components/CreateTodo'
import todoStorage from './components/TodoStorage';

export default {
  name: 'app',
  components: {
    TodoList,
    CreateTodo
  },
  data () {
    return {
      todos: todoStorage.fetch()
    }
  },
  watch: {
    todos: {
      handler: function (todos) {
        todoStorage.save(todos)
      }
    }
  },
  methods: {
    createTodo (newTodo) {
      this.todos.push(newTodo)
      todoStorage.save(newTodo)
    }
  }
}
</script>

<style scoped>
  .m-y-3 {
    margin: 80px 0;
  }
</style>