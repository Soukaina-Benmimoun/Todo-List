<template>
    <div>
       <h2>Modifier un todo</h2>
       <form @submit.prevent="updateTodo">
         <input type="text" v-model="todo.text" />
         <button type="submit">Modifier</button>
       </form>
    </div>
   </template>
   
   <script>
   export default {
    props: ['todo'],
    methods: {
       updateTodo() {
         this.$emit('update', this.todo);
       }
    }
   }
   </script>
   
   <style>
   /* Styles pour TodoModifier.vue */
   </style>
   