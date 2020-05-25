<template>
  <div id="app">
    <h1>Hello World</h1>
    <hr>
    <br>
    <AddTodo
            @add-todo="addTodo"
    />
    <br>
    <TodoList
            v-bind:todos="TodoListArr"
            v-on:remove-todo="removeTodo"
    />

  </div>
</template>

<script>
  import TodoList from './components/TodoList.vue';
  import AddTodo from './components/addTodo';
  export default {
    name: 'App',
    components: {
      TodoList,
      AddTodo
    },
    methods: {
      removeTodo(id) {
        this.TodoListArr = this.TodoListArr.filter(t => t.id !== id)
      },
      addTodo(todo) {
        this.TodoListArr.push(todo);
        console.log('Vova: ', todo.task);
      }
    },
    data() {
      return {
        TodoListArr: [
          {
            id: 1,
            task: 'Learn Vue',
            completed: false,
          },
          {
            id: 2,
            task: 'Hello World',
            completed: false,
          },
          {
            id: 3,
            task: 'My Friend is the best',
            completed: false,
          }
        ]
      }
    }
  }

</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
  ul {
    list-style: none;
  }
</style>
