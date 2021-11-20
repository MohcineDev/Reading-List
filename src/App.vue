<template>
  <div id="#app">

    <h1>Reading List</h1>
    <form @submit.prevent="addNewBook">
      <input v-model="newBook" type="text" placeholder="add New..." required name="newBook">
      <button>
        <svg fill="#fff" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
          <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm1-11a1 1 0 10-2 0v2H7a1 1 0 100 2h2v2a1 1 0 102 0v-2h2a1 1 0 100-2h-2V7z" clip-rule="evenodd">
          </path>
        </svg>
      </button>
    </form>
    <div v-if="books.length" class="btns">
      <button @click="markDone">Mark All Done</button>
      <button @click="cleanBooks">Remove All</button>
    </div>

    <ul>
    <li v-for="(book, i) in books" :key="i">
      <h3 :class="{done:book.done}" @click="toggleDone(book)"> {{book.book}} </h3>
      <button @click="deleteBook(i)">
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
    const newBook = ref("");
    const books = ref([{
      book :"blue ocean strategy",
      done :false
    }]);
    function addNewBook() {
      books.value.push({
        done: false,
        book: newBook.value,
      });
      newBook.value = "";
    }
    function toggleDone(book) {
      book.done = true;
    }
    function deleteBook(i) {
      books.value.splice(i, 1);
    }
    function markDone() {
      books.value.map((book) => (book.done = true));
    }
    function cleanBooks() {
      books.value = [];
    }
    ///make the function availabel
    return {
      addNewBook,
      newBook,
      books,
      toggleDone,
      deleteBook,
      markDone,
      cleanBooks,
    };
  },
};
</script>

<style>
#app {
  font-family:Arial, Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  max-width: 400px;
  margin: auto;
}

button {
  padding: 0;
  border: none;
  cursor: pointer;
  background: #9c78ff;
}

svg {
  width: 30px;
  vertical-align: middle;
  transition: fill 0.3s;
}
form {
  background: #9c78ff;
  display: flex;
  align-items: center;
  width: 400px;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 0 5px #b39af9;
}

input {
  padding: 0 10px;
  border: none;
  height: 30px;
  width: 100%;
  color: #fff;
  background: #9c78ff;
  font-size: 14px;
}
input::placeholder {
  color: #fff;
}
.btns {
  display: flex;
  width: 90%;
  margin: auto;
  border-radius: 0 0 10px 10px;
  overflow: hidden;
}
.btns button {
  width: 100%;
  padding: 10px;
  color: #fafafa;
  font-size: 14px;
  letter-spacing: 1px;
}
.btns button:hover {
  background: #a98bfc;
}
ul {
  padding: 0;
}
li {
  display: block;
  background: #fefefe;
  display: flex;
  justify-content: space-between;
  margin: 5px 0;
  align-items: center;
  box-shadow: 0 0 10px #c5b2fb;
}
li button {
  background: #fafafa;
}
h3 {
  margin: 5px;
  padding: 0 5px;
  flex-grow: 1;
  text-align: left;
  text-transform: capitalize;
}
.done {
  text-decoration: line-through;
}
</style>
