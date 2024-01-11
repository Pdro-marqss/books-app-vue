<script setup>

import { ref, reactive } from 'vue';

import Books from './components/Books.vue';
import BookProgress from './components/BookProgress.vue';
import AddBook from './components/AddBook.vue';

let showAddBookModal = ref(false);

let books = reactive([
  {
    id: crypto.randomUUID(),
    title: "Farenheit 451",
    cover: "https://i.pinimg.com/564x/60/c8/b2/60c8b23701584a543bfa6839dd0ffe5d.jpg",
    isRead: true,
    author: "Ray Bradbury",
  },
  {
    id: crypto.randomUUID(),
    title: "Robin Hood",
    cover: "https://i.pinimg.com/564x/c8/91/56/c89156678051d3d67715532a8f68a209.jpg",
    isRead: true,
    author: "Alexandre Dumas",
  },
  {
    id: crypto.randomUUID(),
    title: "1984",
    cover: "https://i.pinimg.com/564x/04/1c/dd/041cdd9ff00680e9586f645c90f71462.jpg",
    isRead: false,
    author: "George Orwell",
  },
  {
    id: crypto.randomUUID(),
    title: "Flores para Algernon",
    cover: "https://i.pinimg.com/564x/ca/c7/ab/cac7ab4563acb18eb2de5b4f77131088.jpg",
    isRead: false,
    author: "Daniel Keyes",
  },
  {
    id: crypto.randomUUID(),
    title: "Rei Arthur",
    cover: "https://i.pinimg.com/564x/9e/09/26/9e0926830f3e2d95bfe6db047b01c25c.jpg",
    isRead: false,
    author: "Howard pyle",
  },
]);

function toggleIsRead(id) {
  books.forEach((book) => {
    if (book.id === id) {
      book.isRead = !book.isRead;
    }
  })
}

function addBook(newBook) {
  newBook.id = crypto.randomUUID();

  books.push(newBook);
  showAddBookModal.value = false;
}

</script>

<template>
  <div class="container" v-if="!showAddBookModal">
    <h1>📖 Meus Livros</h1>
    <div class="header-btns">
      <button class="btn" @click="showAddBookModal = true">Adicionar Livro +</button>
    </div>

    <div class="books-container">
      <BookProgress :books="books" />

      <Books @toggleIsRead="toggleIsRead" :books="books" />

      <!-- <BookProgress :books="books" /> -->

    </div>
  </div>
  <div class="container" v-else="">
    <AddBook @addBook="addBook" @closeAddBook="showAddBookModal = false" />
  </div>
</template>

<style scoped></style>
