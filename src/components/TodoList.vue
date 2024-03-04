<template>
    <div id="app">
        <h2>Todo List</h2>
        <div>
          <input type="text" v-model="newTodo" @keyup.enter="addTodo">
          <button @click="addTodo">Ajouter</button>
        </div>
        <ul>
          <li v-for="todo in todos" :key="todo.id">
            <span>{{ todo.text }}</span>
            <button @click="selectTodoForUpdate(todo)">Update</button>
            <button @click="removeTodo(todo)">delete</button>
          </li>
        </ul>
        <todo-modifier v-if="todoToUpdate" :todo="todoToUpdate" @update="updateTodo"/>
    </div>
   </template>
   
   <script>
   import TodoModifier from './TodoModifier.vue'; 
   
   export default {
    components: {
       TodoModifier
    },
    data() {
       return {
         newTodo: '',
         todos: [],
         todoToUpdate: null 
       };
    },
    methods: {
       addTodo() {
         if (this.newTodo) {
           this.todos.push({
             id: this.todos.length,
             text: this.newTodo
           });
           this.newTodo = '';
         }
       },
       removeTodo(todo) {
         this.todos = this.todos.filter(t => t.id !== todo.id);
       },
       updateTodo(updatedTodo){
         const index = this.todos.findIndex(t => t.id === updatedTodo.id);
         if (index !== -1) {
           this.todos.splice(index, 1, updatedTodo); 
         }
         this.todoToUpdate = null;
       },
       selectTodoForUpdate(todo) {
         this.todoToUpdate = todo;
       }
    }
   }
   </script>
   <style>
   #app {
     display: flex;
     flex-direction: column;
     align-items: center;
   }
   
   input {
     margin-bottom: 10px;
     padding: 10px;
     font-size: 20px;
     border: none;
     border-radius: 5px;
     background-color: #eee;
   }
   
   ul {
     list-style: none;
     padding: 0;
   }
   
   li {
     margin-bottom: 10px;
   }
   
   span {
     margin-right: 10px;
   }
   
   button {
     padding: 10px;
     border: none;
     border-radius: 5px;
     background-color: red;
     color: white;
     cursor: pointer;
   }
   </style>
   