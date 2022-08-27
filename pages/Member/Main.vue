<template lang="pug">
section
  Navbar
  .contents.space-y-3
    div(class="w-full bg-white shadow-md")
      .flex.items-center.pt-6.mb-1
        h1(href="#" class="text-green-text font-extrabold ml-14 text-lg") หนังสือใหม่
        <img src="@/assets/images/clock.png" class="w-5 h-5 ml-2 mb-1">
      .divbgwhite.shadow-md
          div(class="pt-4 mx-6 justify-self-start wrapper space-y-4")
            BookCardIndex(
              v-for="book in sortId()"
              :key="book.bname"
              :product="book"
              )
    div(class="w-full bg-white shadow-md")
      .flex.items-center.pt-6.mb-1
        h1(href="#" class="text-green-text font-extrabold ml-14 text-lg") หนังสือยอดนิยม
        <img src="@/assets/images/star.png" class="w-5 h-5 ml-2 mb-1">
      .divbgwhite.shadow-md
          div(class="pt-4 mx-6 justify-self-start wrapper space-y-4")
            BookCardIndex(
              v-for="book in sortRating()"
              :key="book.bname"
              :product="book"
              )

</template>

<script>
import { defineComponent } from '@nuxtjs/composition-api'
import Navbar from '~/components/Member/Navbar.vue'
import BookCardIndex from '@/components/BookCardIndex.vue'

export default defineComponent({
  components: {
    Navbar,
    BookCardIndex,
  },
  data() {
    return {
      books: [],
    }
  },
  async fetch() {
    this.books = await fetch(
      'http://localhost:8080/books'
    ).then((res) => res.json())
  },
  methods: {
    sortId (){
      if( this.books===undefined) {
        return []
      }
      return this.books.slice().sort(function(a, b){
        return (a.bookId > b.bookId) ? -1 : 1;
      });
    },
    sortRating (){
      if( this.books===undefined) {
        return []
      }
      return this.books.slice().sort(function(a, b){
        return (a.rating > b.rating) ? -1 : 1;
      });
    }
  }
})
</script>

<style>
.divbgwhite{
  height: 250px;
  width: 100%;
  background-color: white;
}

body{
  background-color: lightgray;
  
}

.wrapper{
  max-height: 200px;
  overflow-x: hidden;
  overflow-y: auto;
}

.wrapper::-webkit-scrollbar{
  width: 0;
  height: 12px;
}

.wrapper .item{
  line-height: 300px;
  text-align: center;
  background-color: #ddd;
}

.wrapper::-webkit-scrollbar:hover {
  background-color: lightslategray;
}
</style>
