<template>
  <div>
    <h1>test</h1>
    <router-link to="/">main</router-link>
    <AddTodo @add-todo="addTodo" />
    <select v-model="filter"><option value="all" selected>all</option><option value="completed">completed</option><option value="not">not</option></select>
    <Loader v-if="loader" />
    <TodoList v-else-if="ft.length" v-bind:todos="ft" @remove-todo="removeTodo"/>
    <p v-else>hhhhhhhhhhhhhhhhhhhhh</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList';
import AddTodo from '@/components/AddTodo';
import Loader from '@/components/Loader';
export default {
  name: 'App',
  data() {
    return {
      todos: [

      ], 
      loader: true, 
      filter: "all"
    }
  },
//  watch: {
  //    filter(value) {
    //      console.log(value);

      //}
  //},
  computed: {
      ft() {
         if (this.filter == "all") {
             return this.todos;
         } if (this.filter === "completed") {
            return this.todos.filter(t => t.completed);
         } else
         return this.todos;
        
      }
  },

  mounted(){
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
    .then(response => response.json())
     .then(json => {this.todos= json;this.loader = false;
     })
  },
  components: {
    TodoList, AddTodo, Loader
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
    addTodo(todo){
      this.todos.push(todo);

    }

  }
}
</script>
