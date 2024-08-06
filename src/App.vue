<template>
  <div class="container">
     <h1>Vue Todo App</h1>
   <form @submit.prevent="addNewTodo">
     <label>New Todo</label>
     <input v-model="newTodo" name="newTodo">
     <button>Add New Todo</button>
   </form>
   <button @click="removeAllTodos">Remove All</button>
   <button @click="markAllDone">Mark All Done</button>
   <ul>
      <li v-for="(todo, index) in todos" :key="todo.id" class="todo">
        <h3 :class="{ done: todo.done }" @click="toggleDone(todo)">{{todo.content}}</h3>
        <button @click="removeTodo(index)">Remove Todo</button>
      </li>
   </ul>
  </div>
  
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const newTodo = ref('');
    const todos = ref([]);

    function addNewTodo() {
      todos.value.push({
        done: false,
        content: newTodo.value,
      });
      newTodo.value = '';
    }

    function toggleDone(todo) {
      todo.done = !todo.done;
    }

    function removeTodo( index ) {
      todos.value.splice( index, 1);
    }

    function markAllDone() {
        todos.value.forEach((todo) => todo.done = true); 
    }

    function removeAllTodos () {
       todos.value = [];
    }

    return {
      todos,
      newTodo,
      addNewTodo,
      toggleDone,
      removeTodo,
      markAllDone,
      removeAllTodos,
    };
  }
}

</script>

<style>
body {
  font-family: sans-serif;
  padding-top: 1rem;
  padding-bottom: 1rem;
  font-size: 2rem;
  margin: 0 auto;
  width: 80%;
  margin: 0 auto;

}
form {
  display: flex;
  flex-direction: column;
}
input, textarea, button, p, div, section, article, select {
  display: 'block';
  /* width: 200%; */
  font-family: sans-serif;
  font-size: 1rem;
  padding: 17px;
  margin: 0.5em;
}
.container {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    margin-top: 100px;
    background-color: cadetblue;
}
.container button {
  width: 300px;
}
button {
  color: rgb(142, 133, 143);
  border-radius: 20px;
  border: none;
  cursor: pointer;
}
h1 {
  font-size: 40px;
  
  
}
.todo {
  cursor: pointer;
}
.done {
   text-decoration: line-through;
}

</style>
