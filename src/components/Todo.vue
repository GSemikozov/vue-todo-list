<template>
  <div class='list-group list-group-flush'>
    <div class='list-group-item' v-show="!isEditing">
      <div class="pull-left">
        <h4>
          {{ todo.title }}
        </h4>
        <p>
          {{ todo.description }}
        </p>
      </div>
      <div class='extra-content'>
          <span class='btn btn-sm' @click="showForm">
          <i class='fa fa-pencil-square-o'></i>
        </span>
        <span class='btn btn-sm' @click="deleteTodo(todo)">
          <i class='fa fa-trash-o'></i>
        </span>
      </div>
      <div class="card-block clearfix">
        <a class='card-link text-success' disabled v-show="!isEditing &&todo.done">
          <i class='fa fa-check-o'></i> Completed
        </a>
        <a class='card-link' @click="completeTodo(todo)" v-show="!isEditing && !todo.done">
          <i class='fa fa-pencil'></i> Mark as a completed
        </a>
      </div>
    </div>
    <div class='list-group-item' v-show="isEditing">
      <form>
        <div class='form-group'>
          <label>Title</label>
          <input type='text' class='form-control' v-model="todo.title">
        </div>
        <div class='form-group'>
          <label>Description</label>
          <input type='text' class='form-control' v-model="todo.description">
        </div>
        <button type="button" class='btn btn-sm btn-primary save-todo-list-btn' @click="saveTodo(todo)">
          Save to storage
        </button>
        <button type='button' class='btn btn-sm btn-outline-primary' @click="hideForm">
          <i class='fa fa-close'></i> Close
        </button>
      </form>
    </div>
  </div>
</template>

<script type="text/javascript">
  import todoStorage from './TodoStorage'
  import TodoList from './TodoList'
  export default {
    props: ['todo', 'todos'],
    components: {
      TodoList
    },
    data () {
      return {
        isEditing: false
      }
    },
    methods: {
      completeTodo (todo) {
        this.$emit('complete-todo', todo)
      },
      deleteTodo (todo) {
        this.$emit('delete-todo', todo)
      },
      saveTodo (todo) {
        this.$emit('save-todo', todo)
        this.isEditing = false
      },
      showForm () {
        this.isEditing = true
      },
      hideForm () {
        this.isEditing = false
      }
    }
  }
</script>

<style scoped>
  .extra-content {
    float: right;
  }
  .extra-content .btn {
    cursor: pointer;
  }
  .clearfix {
    clear: both;
  }
  .card-link {
    margin-left: 0;
    cursor: pointer;
  }
  .extra-content .btn, .card-link:hover {
    opacity: .8;
  }
  .card-link:hover {
    text-decoration: underline !important;
  }
  a[disabled] {
    pointer-events: none;
  }
</style>