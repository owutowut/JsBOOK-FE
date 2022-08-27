<template lang="pug">
section.NavbarMenu.shadow-md
  div(class="w-full h-16 bg-green-navbar")
    div.grid.grid-cols-6.items-center.pt-1
      .logo.col-span-2
        div(class="flex items-center")
          img(src="~@/assets/images/JBlogo.svg" class="h-12 w-14 ml-8 opacity-95 mt-1")
          a(href="/Member/Main" class="text-white opacity-95 font-extrabold text-2xl mt-1") JAMIE's BOOK
        div.spacebox
      .freespace.col-span-3
      Dropdown.justify-self-start.ml-6
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