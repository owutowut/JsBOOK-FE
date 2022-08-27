<template lang="pug">
section
  Navbar 
  .divbgwhite.shadow-md
      div(class="ml-12 pt-5")
        select(v-model="searchCategory" class="text-center text-gray-800 rounded w-44 h-9 cursor-pointer border-2")
          option(disabled, value) เลือกหมวดหมู่
          option การเขียนโปรแกรม
          option วรรณกรรม
          option การเงินการลงทุน
      div(class="mt-4 mx-6 justify-self-start wrapper space-y-4")
        BookCard(
          v-for="book in filteredCategory"
          :key="book.bname"
          :product="book"
          )
</template>

<script>
import { defineComponent } from '@nuxtjs/composition-api'
import BookCard from '~/components/BookCard.vue'
import Navbar from '~/components/Librarian/Navbar.vue'

export default defineComponent({
  components: {
    Navbar,
    BookCard,
  },
  data() {
    return {
      books: [],
      searchCategory: 'การเขียนโปรแกรม',
    }
  },
  async fetch() {
    this.books = await fetch(
      'http://localhost:8080/books'
    ).then((res) => res.json())
  },
  computed:{
    filteredCategory(){
      return this.books.filter((book) => {
        return book.category.match(this.searchCategory);
      });
    },
  }
})
</script>

<style>
body {
  background-color: lightgray;
}

.wrapper{
  max-height: 500px;
  overflow-x: hidden;
  overflow-y: auto;
}

img{
  height: 160px;
}

.divbgwhite{
  height: 610px;
  width: 100%;
  background-color: white;
}
</style>