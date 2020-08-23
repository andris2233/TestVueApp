<template>
    <div class="wrapper">
        <div class="header">
            <h2>Todo App</h2>
            <TodoForm @create-todo="createTodo"/>
        </div>
        
        <ul>
            <TodoItem 
                v-for="(todo, i) of todos"
                v-bind:todo="todo"
                v-bind:index="i"
                v-bind:key="todo.id"
                v-on:remove-todo="removeTodo"
            />
            <div v-if="todos.length === 0" class="empty-todos">
                Дела отсутствуют!
            </div>
        </ul>
    </div>
</template>

<script>
import TodoItem from '@/components/TodoItem';
import TodoForm from '@/components/TodoForm';
export default {
    props: ['todos'],
    components: {
        TodoItem, TodoForm
    },
    methods: {
        removeTodo(id){
            this.$emit('remove-todo', id);
        },
        createTodo (todo){
            this.$emit('create-todo', todo);
        }
    }
}
</script>

<style scoped>
ul {
    list-style: none;
    width: 100%;
    height: 100%;
    margin: 0;
    padding: 0;
    border-radius: 5px;
    background: white;
    padding: 7px;
    box-sizing: border-box;
    overflow: hidden;
}
.wrapper {
    width: 100%;
    max-width: 600px;
    min-width: 350px;
    border-radius: 7px;
    box-shadow: 0 0 10px 2px #dadada;
    padding: 10px 4px 4px 4px;
    background: #3BA8C6;
}

.empty-todos{
    padding: 5px 0 6px 0;
    border-radius: 5px;
    color: #2c3e50;
    font-weight: bold;
}

h2{
    color: white;
    font-weight: bold;
    margin: 0;
}

.header{
    display: flex;
    align-items: flex-end;
    justify-content: space-between;
    padding: 5px 7px 8px 7px;
}
</style>