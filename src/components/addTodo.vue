<template>
    <form @submit.prevent="onSubmit">
        <input type="text" v-model="title">
        <button type="submit">Create</button>
    </form>
</template>

<script>
    export default {
        data() {
          return {
              title: ''
          }
        },
        methods: {
            onSubmit() {
                console.log('Test:', this.title);
                if(this.title.trim()) {
                    const newTodo = {
                        id: Date.now(),
                        task: this.title,
                        completed: false
                    };
                    this.$emit('add-todo', newTodo);
                    this.title = ''
                }
            }
        }
    }
</script>

<style scoped>
    form {
        display: flex;
        justify-content: center;
    }
    button {
        margin-left: 14px;
    }
</style>