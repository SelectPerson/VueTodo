<template>
    <div>
        <h2>List To Do</h2>
        <router-link to="/">Home</router-link>
        <hr>
        <br>

        <AddTodo
                @add-todo="addTodo"
        />
        <br>
        <select v-model="filter">
            <option value="all">All</option>
            <option value="completed">Completed</option>
            <option value="not-completed">No Completed</option>

        </select>
        <br><br>
        <Loader v-if="loading" />
        <TodoList
                v-else-if="filteredTodos.length"
                v-bind:todos="filteredTodos"
                v-on:remove-todo="removeTodo"
        />
        <p v-else>No todos!</p>
    </div>
</template>

<script>
    import TodoList from '@/components/TodoList.vue';
    import AddTodo from '@/components/addTodo';
    import Loader from '@/components/Loader';
    export default {
        name: 'App',
        components: {
            TodoList,
            AddTodo,
            Loader
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
        // watch: {
        //   filter(value) {
        //       console.log(value);
        //   }
        // },
        computed: {
            filteredTodos() {
                if(this.filter === 'all') {
                    return this.TodoListArr;
                }
                if(this.filter === 'completed') {
                    return this.TodoListArr.filter(t => t.completed);
                }
                if(this.filter === 'not-completed') {
                    return this.TodoListArr.filter(t => !t.completed);
                }
            }
        },
        mounted() {
            setTimeout(() => {
                this.loading = false;
            },100);
            // fetch('https://jsonplaceholder.typicode.com/todos')
            //         .then(response => response.json())
            //         .then(json => {
            //           this.TodoListArr = json;
            //           console.log(json);
            //         });
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
                ],
                loading: true,
                filter: 'all'
            }
        }
    }
</script>