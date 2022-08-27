<template lang="pug">
section.bg-silver
  Navbar
  div.flex
    Sidebar
    div.my-8.pt-8.pb-4.pl-8.bg-white.opacity-95.text-gray-800.w-full.h-full.mx-8.mt-6.rounded
      h1.font-semibold.text-2xl.pl-4 การยืม
      div.mt-2
        hr
      div.grid-cols-2.flex.pt-4.space-x-4.h-14.mt-2.ml-1
        button.btn.font-bold.py-2.px-4.rounded.items-center.shadow-md(class="hover:shadow-none" onclick="document.location='/Librarian/Edit/NewLoans'")
          span + เพิ่ม
        div.flex.space-x-2
          input.rounded-lg.border.px-4.py-3.w-80(placeholder="ค้นหาด้วยเลขบัตรประชาชน . . . " class=" focus:bg-white" v-model="searchIDcard")

      div.tablebox.mt-6.mb-6.overflow-y-auto.rounded-xl.mr-10
        div.mr-4.rounded-xl
          table.w-full
            thead
              tr.border
              th.px-2.py-3.text-left.text-xs.font-semibold.uppercase.tracking-wider.border.text-center  เลขบัตรประชาชน
                th.py-3.text-left.text-xs.font-semibold.uppercase.tracking-wider.border.text-center  รหัสหนังสือ
                th.px-4.py-3.text-left.text-xs.font-semibold.uppercase.tracking-wider.border.text-center  วันที่ยืม
                th.px-4.py-3.text-left.text-xs.font-semibold.uppercase.tracking-wider.border.text-center  วันครบกำหนด
                th.px-4.py-3.text-left.text-xs.font-semibold.uppercase.tracking-wider.border.text-center  วันที่คืน
                th.px-4.py-3.text-left.text-xs.font-semibold.uppercase.tracking-wider.border.text-center  สถานะ
                th.px-4.py-3.text-left.text-xs.font-semibold.uppercase.tracking-wider.border.text-center  การจัดการ
            tbody(
                  v-for="loan in filtered"
                  :key="loan._id"
                  )
              tr
                td.px-2.py-5.border.text-sm.text-center 
                  p {{loan.IDcard}}
                td.py-5.border.text-sm.text-center 
                  a(:href="`/Librarian/View/Book/${loan.bid}`" class="text-blue-700") {{loan.bid}}
                td.px-4.py-5.border.text-sm.text-center
                  p {{loan.IsDate}}
                td.px-4.py-5.border.text-sm.text-center
                  p {{loan.DueDate}}
                td.px-4.py-5.border.text-sm.text-center
                  p {{loan.ReDate}}
                td.px-4.py-5.border.text-sm.font-semibold.text-center
                  p(v-if="loan.lstatus=='ล่าช้า'" class=" text-red-700").break-normal.whitespace-nowrap {{loan.lstatus}}
                  p(v-else-if="loan.lstatus=='กำลังดำเนินการ'" class=" text-yellow-700").break-normal.whitespace-nowrap {{loan.lstatus}}
                  p(v-else class=" text-green-700").break-normal.whitespace-nowrap {{loan.lstatus}}
                td.px-5.py-5.border.text-sm.border.space-x-2.text-center
                    a.text-center(:href="`/Librarian/Edit/Loans/${loan._id}` " title="title" class="text-blue-500") Edit
                    button(class="text-red-500" @click="deleteloans(loan._id)") Delete
</template>

<script>
import { defineComponent } from '@nuxtjs/composition-api'
import axios from "axios"
import Sidebar from '~/components/Librarian/Sidebar.vue'
import Navbar from '~/components/Librarian/EditMenu.vue'

export default defineComponent({
  components : {
    Sidebar,
    Navbar,
  },
  data() {
    return {
      loans: [],
      searchIDcard: '',
    }
  },
  async fetch() {
    this.loans = await fetch(
      'http://localhost:8080/loans/'
    ).then((res) => res.json())
  },
  computed:{
    filtered(){
      
      if(this.searchIDcard) {
        return this.loans.filter((loan) => loan.IDcard.match(this.searchIDcard));
      }
      else{
        return this.loans
      }
      },
    
    },
  methods: {
    async deleteloans(id) {
    if(confirm(`คุณต้องการลบข้อมูลนี้หรือไม่`)){
      await axios.delete(`http://localhost:8080/loans/${id}`)
      location.reload()
    }
    }
  }
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
  height: 450px;
}

body {
  background-color: silver;
}
</style>