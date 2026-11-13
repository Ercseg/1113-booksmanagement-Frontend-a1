<script setup>
import { getBooks, createBook } from "../api/books.js";
</script>

<script>
export default {
  name: "BooksManager",
  data() {
    return {
      books: [],
      newBook: {
        title: "",
        author: "",
        year: 2000,
      },
    };
  },
  methods: {
    async loadBooks() {
      this.books = await getBooks();
    },
    async addBook(book){
      await createBook(book);
      await this.loadBooks();
    },
    async submitCreateBook(){
      await this.addBook(this.newBook);
    }
  },
  mounted() {
    this.loadBooks();
  },
};
</script>

<template>
  <main class="flex justify-center items-center flex-col">
    <h1 class="">Könyvtár kezelőfelülete</h1>

    <form
    @submit.prevent="submitCreateBook"
      class="w-full my-10 border-2 border-stone-200 p-3 flex flex-col rounded-xl"
    >
      <div class="flex flex-col">
        <label for="title" class="">Könyv cím:</label>
        <input
          v-model="newBook.title"
          type="text"
          name="title"
          id=""
          class="border-2 border-stone-200 rounded-lg py-1 px-2"
        />
      </div>

      <div class="flex flex-col">
        <label for="author" class="">Könyv Szerzője:</label>
        <input
          v-model="newBook.author"
          type="text"
          name="author"
          id=""
          class="border-2 border-stone-200 rounded-lg py-1 px-2"
        />
      </div>

      <div class="flex flex-col">
        <label for="year" class="">Könyv megjelenési éve:</label>
        <input
          v-model="newBook.year"
          type="number"
          name="year"
          id=""
          class="border-2 border-stone-200 rounded-lg py-1 px-2"
        />
      </div>

      <button
        type="submit"
        class="bg-blue-500 text-white rounded-lg py-1 px-2 mt-3"
      >
        Könyv hozzáadása
      </button>
    </form>
    <table class="">
      <thead class="">
        <tr class="">
          <th class="">azonosito</th>
          <th class="">címe</th>
          <th class="">szerző</th>
          <th class="">megjelenés éve</th>
          <th class="">műveletek</th>
        </tr>
      </thead>

      <tbody class="">
        <tr v-for="book in books" :key="book.id" class="">
          <td class="">{{ book.id }}</td>
          <td class="">{{ book.title }}</td>
          <td class="">{{ book.author }}</td>
          <td class="">{{ book.year }}</td>
          <td class="">-</td>
        </tr>
      </tbody>
    </table>
  </main>
</template>
