<template lang="pug">
section.bg-silver
  Navbar
  div.flex
    Sidebar
    div.my-8.pt-8.pb-4.pl-8.bg-white.opacity-95.text-gray-800.w-full.h-full.mx-8.mt-6.rounded
      h1.font-semibold.text-2xl.pl-4 การยืม
      div.mt-2
        hr

      div.tablebox.mt-6.mb-6.overflow-y-auto.rounded-xl.mr-10
        div.mr-4.rounded-xl
          table.w-full
            thead
              tr.border
                th.px-2.py-3.text-left.text-xs.font-semibold.uppercase.tracking-wider.border.text-center  ชื่อผู้ยืม
                th.py-3.text-left.text-xs.font-semibold.uppercase.tracking-wider.border.text-center  รหัสหนังสือ
                th.px-4.py-3.text-left.text-xs.font-semibold.uppercase.tracking-wider.border.text-center  วันที่ยืม
                th.px-4.py-3.text-left.text-xs.font-semibold.uppercase.tracking-wider.border.text-center  วันครบกำหนด
                th.px-4.py-3.text-left.text-xs.font-semibold.uppercase.tracking-wider.border.text-center  วันที่คืน
                th.px-4.py-3.text-left.text-xs.font-semibold.uppercase.tracking-wider.border.text-center  สถานะ
            tbody(
                  v-for="loan in filtered"
                  :key="loan._id"
                  )
              tr
                td.px-2.py-5.border.text-sm.text-center 
                  p {{firstname}}  {{lastname}}
                td.py-5.border.text-sm.text-center 
                  a(:href="`/Member/View/Book/${loan.bid}`" class="text-blue-700") {{loan.bid}}
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
</template>

<script>
import { defineComponent } from '@nuxtjs/composition-api'
import axios from 'axios'
import Sidebar from '~/components/Member/Sidebar.vue'
import Navbar from '~/components/Member/EditMenu.vue'

export default defineComponent({
  components : {
    Sidebar,
    Navbar,
  },
  data() {
    return {
      loans: [],
      IDcard:'',
      firstname:'',
      lastname:'',
    }
  },
  async fetch() {
    this.loans = await fetch(
      'http://localhost:8080/loans/'
    ).then((res) => res.json())
    console.log(this.loans);
  },
  computed:{
    filtered(){
      
      if(this.IDcard) {
        return this.loans.filter((loan) => loan.IDcard.match(this.IDcard));
      }
      else{
        return this.loans
      }
      },
    
    },
  async mounted() {
    const res=await axios.get('http://localhost:8080/profile', {
      headers: { authorization: `Bearer ${localStorage.getItem('token')}` },
    })
    this.IDcard=res.data.IDcard
    this.firstname=res.data.firstname
    this.lastname=res.data.lastname
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
  height: 440px;
}

body {
  background-color: silver;
}
</style>