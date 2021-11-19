<template>
<div id="#app">

  <h1>Reading List</h1>
  <form @submit.prevent="addNewTodo">
    <input v-model="newTodo" type="text" placeholder="add New..." name="newTodo">
    <button>
      <svg fill="#2c3e50" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm1-11a1 1 0 10-2 0v2H7a1 1 0 100 2h2v2a1 1 0 102 0v-2h2a1 1 0 100-2h-2V7z" clip-rule="evenodd">
        </path>
      </svg>
    </button>
  </form>
  <div class="btns">
    <button @click="markDone">Mark All Done</button>
    <button @click="cleanTodos">Remove All</button>
  </div>
  <ul>

   <li v-for="(todo, i) in todos" :key="i">
    <h3 :class="{done:todo.done}" @click="toggleDone(todo)"> {{todo.content}} </h3>
    <button @click="deleteTodo(i)">
      <svg fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
        <path fill-rule="evenodd" d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z" clip-rule="evenodd">
      </path>
      </svg>
    </button>
    </li>
  </ul>
</div>

</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    //object wrapper
    const newTodo = ref("");
    const todos = ref([]);
    function addNewTodo() {
      todos.value.push({
        done: false,
        content: newTodo.value,
      });
      newTodo.value = "";
    }
    function toggleDone(todo) {
      todo.done = true;
    }
    function deleteTodo(i) {
      todos.value.splice(i, 1);
    }
    function markDone() {
      todos.value.map((todo) => (todo.done = true));
    }
    function cleanTodos() {
      todos.value = [];
    }
    ///make the function availabel
    return {
      addNewTodo,
      newTodo,
      todos,
      toggleDone,
      deleteTodo,
      markDone,
      cleanTodos,
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  max-width:400px ;
  margin: auto;
}
ul{
  padding: 0;
}
li {
  display: block;
  background: #fefefe;
  display: flex;
  justify-content: space-between;
  margin: 5px 0;
  align-items: center;
}
h3{
  margin: 5px;
  padding: 0 5px;
}
.done {
  text-decoration: line-through;
}
button {
  padding: 0;
  background: #fafafa;
  border: none;
  cursor: pointer;
}
input {
  padding: 0 10px;
  border: none;
  height: 30px;
  width: 100%;
  background: #fafafa;
}
svg {
  width: 30px;
  vertical-align: middle;
  transition:fill 0.3s;
}
svg:hover {
  fill: #37536e;
}
form {
  background: #fafafa;
  display: flex;
  align-items: center;
  width: 400px;
  border-radius: 10px;
  overflow: hidden;
}
.btns{
  display: flex;
  width: 90%;
  margin: auto;
  border-radius: 0 0 10px 10px;
  overflow: hidden;
}
.btns button{
  width: 100%;
  padding: 10px;
}
.btns button:hover{
  background: #fff;
}
</style>
