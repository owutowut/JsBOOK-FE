<template lang="pug">
section.bg-silver.min-h-screen
  Navbar
  div.flex
    Sidebar
    div.my-8.pt-8.pb-4.pl-8.bg-white.opacity-95.text-gray-800.w-full.h-full.mx-8.mt-6.rounded
      h1.font-semibold.text-2xl.pl-4 หนังสือ
      div.mt-2
        hr
      div.grid-cols-2.flex.pt-4.space-x-4.h-14.mt-2
        div.flex.space-x-2
          input.rounded-lg.border.px-4.py-3.w-80(placeholder="ค้นหาด้วยรหัสหนังสือ . . . " class=" focus:bg-white" v-model="searchName")

      div.tablebox.mt-6.mb-6.overflow-y-auto.rounded-xl.mr-10
        div.mr-4.rounded-xl
          table
            thead
              tr.border
                th.px-5.py-3.text-left.text-xs.font-semibold.uppercase.tracking-wider.border.text-center  ปกหนังสือ
                th.px-5.py-3.text-left.text-xs.font-semibold.uppercase.tracking-wider.border.text-center  ชื่อ
                th.px-5.py-3.text-left.text-xs.font-semibold.uppercase.tracking-wider.border.text-center  ผู้แต่ง
                th.px-5.py-3.text-left.text-xs.font-semibold.uppercase.tracking-wider.border.text-center  รหัสหนังสือ
                th.px-5.py-3.text-left.text-xs.font-semibold.uppercase.tracking-wider.border.text-center  สถานะ
                th.px-5.py-3.text-left.text-xs.font-semibold.uppercase.tracking-wider.border.text-center  จัดการข้อมูล
            tbody(
                  v-for="book in filtered"
                  :key="book._id"
                  )
              tr
                td.px-5.py-5.border.text-sm
                  .flex.items-center
                    .flex.w-20.h-24
                      img.jpg.w-full.h-full(:src="book.cover" alt="")
                td.px-5.py-5.border.text-sm.text-center 
                  p {{book.bname}}
                td.px-5.py-5.border.text-sm.text-center 
                  p.break-normal.whitespace-nowrap {{book.author}}
                td.px-5.py-5.border.text-sm.text-center
                  p {{book._id}}
                td.px-5.py-5.border.text-sm.font-semibold.text-center(:class="`${book.status=='ไม่พร้อมใช้งาน'?' text-red-700 ':' text-green-700 '}`")
                  p.break-normal.whitespace-nowrap {{book.status}}
              
                td.px-5.py-5.border.text-sm.border
                  .flex.space-x-3.pl-6
                    a.text-center(:href="`/View/Book/${book._id}` " title="title" class="text-blue-500") View
</template>

<script lang="js">
import { defineComponent } from '@nuxtjs/composition-api'
// eslint-disable-next-line @typescript-eslint/no-unused-vars
import Vue from 'vue'
// import axios from "axios"
import Sidebar from '../../components/Member/Sidebar.vue'
import Navbar from '../../components/Member/EditMenu.vue'


export default defineComponent({
  components : {
    Sidebar,
    Navbar,
  },
  data() {
    return {
      books: [],
      searchName: '',
    }
  },
  async fetch() {
    this.books = await fetch(
      'http://localhost:8080/books/'
    ).then((res) => res.json())
    console.log(this.books);
  },
  computed:{
    filtered(){
      if(this.searchName) {
        return this.books.filter((book) => book._id.match(this.searchName));
      }
      else{
        return this.books
      }
      },
    },
  
})
</script>


<style lang="postcss" scoped>
.btn {
  font-size: 16px;
  color: #fff;
  background-color: #409eff;
  border-color: #409eff;
  border-radius: 6px;
}

.warn {
  color: red;
}

.tablebox {
  height: 460px;
}

body {
  background-color: silver;
}
</style>
