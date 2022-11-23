<template>
  <div class="bg-gray-600 text-white w-1/2 m-auto mt-12">
   <div class="text-center border-b-2 border-black py-4">
     <h1 class="text-3xl py-4">Unsere Todos</h1>
     <p class="text-x1" v-if="openTodos.length > 0">Offenen Todos: {{ openTodos.length }}</p>
     <p class="text-x1">Keine Todos, gratuliere!</p>
     <div class="mt-4">
       <input type="text" class="py-2 w-2/3 text-black" v-model="newTodo">
       <button class="bg-red-400 py-2 w-1/3" @click="addTodo">Add Todo</button>
     </div>
   </div>
   <div v-for="(todo, index) in todos" :key="todo.todo">
     <Todo 
     :todoprop="todo" 
     :todoIndex="index" 
     @toggledone-index="toggleDone" 
     @removetodo-index="deleteTodo" />
   </div>


  </div>
</template>

<script>
import Todo from './components/Todo.vue'

export default {
  name: 'App',
  data() {
    return {
      newTodo: "",
      todos: []
    }
  },
  methods: {
   toggleDone(index) {
     this.todos[index].done = !this.todos[index].done;
     this.storeTodos();
   },
   deleteTodo(index) {
     this.todos.splice(index, 1);
     this.storeTodos();
   },
   addTodo() {
    if (this.newTodo.trim() === "") {
      return;
    }
    this.todos.push({todo:this.newTodo, done: false });
    this.storeTodos();
   },
   storeTodos() {
    localStorage.setItem("todos", JSON.stringify(this.todos))
   }
  },
  mounted() {
    let data = localStorage.getItem("todos");
    if (data !== "" && data !== null) {
      this.todos = JSON.parse(data);
    } else {
      this.todos = [];
    }
    
  },
  computed: {
    openTodos() {
      const openTodos = this.todos.filter((todo) => {
        return !todo.done;
      });
      return openTodos
    }
  },
  components: {
    Todo
  }
}
</script>

