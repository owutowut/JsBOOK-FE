<template lang="pug">
section
  div(class="w-full h-16 bg-green-navbar")
    div.grid.grid-cols-6.items-center.pt-1
      .logo.col-span-2
        div(class="flex items-center")
          img(src="~@/assets/images/JBlogo.svg" class="h-12 w-14 ml-8 opacity-95 mt-1")
          a(href="/" class="text-white opacity-95 font-extrabold text-2xl mt-1") JAMIE's BOOK
        div.spacebox
      .freespace.col-span-3
      Dropdown.justify-self-start.ml-6

  div(class="w-full h-12 bg-white flex items-center shadow-md mb-3 space-x-1")
      div(class="hover:bg-silver w-10% h-50% rounded-md items-center ml-8")
        a(href="/" class="text-green-text font-extrabold text-lg px-3 py-2") หน้าแรก
      div(class="hover:bg-silver w-10% h-50% rounded-md items-center")
        a(href="/Category" class="text-green-text font-extrabold text-lg px-3 py-2") หมวดหมู่
</template>

<script>
import { defineComponent } from '@nuxtjs/composition-api'
import Dropdown from '@/components/Member/Dropdown.vue'

export default defineComponent({
  components: {
    Dropdown,
  },
})
</script>