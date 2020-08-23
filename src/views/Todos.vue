<template>
  <div>
    <h2>Todo App</h2>
    <hr>
    <div class="content">
      <TodoList 
        v-bind:todos="todos"
        @remove-todo="removeTodo"
        @create-todo="createTodo"
      />
    </div>
    
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
export default {
  name: 'App',
  data(){
    return {
      todos: []
    }
  },
  components: {
    TodoList
  },
  mounted(){
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
    .then(response => response.json())
    .then(json => this.todos = json);
  },
  methods:{
    removeTodo(id){
      this.todos = this.todos.filter(item => item.id !== id);
    },
    createTodo(todo){
      this.todos.push(todo);
    }
  }
}
</script>

<style>

.content{
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>