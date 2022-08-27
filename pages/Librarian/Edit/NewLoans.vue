<template lang="pug">
section.bg-silver.h-full
  Navbar
  div.flex
    Sidebar
    div.my-8.pt-8.pb-4.pl-14.bg-white.opacity-95.text-gray-800.w-full.h-full.mx-8.mt-6.rounded-xl
      div.space-y-3
          .text-black.text-xl.font-bold.pl-4 เพิ่มการยืม
          hr
          div.pl-2.pt-2
                form(@submit.prevent="formSubmit")
                  div
                    div.grid-cols-2.flex.space-x-14
                      div.space-y-3
                        div
                          label.block.w-28.mb-1 รหัสหนังสือ
                          input.border.rounded.w-96.py-2.px-3.text-grey-darker(type="text" v-model="bid" required)
                        div.pt-2
                          label.block.text-grey-darker.text-sm.font-bold.mb-2 เลขบัตรประชาชน :
                          input.border.rounded.w-96.py-2.px-3.text-grey-darker(type="text" placeholder="" v-model="IDcard" required pattern="[0-9]{13}" maxlength="13" title="กรุณาป้อนเลขบัตรประชาชน 13 หลัก")
                      div.space-y-3
                        div
                          label.block.text-grey-darker.text-sm.font-bold.mb-2 วันที่ยืม :
                          input.border.rounded.w-96.py-2.px-3.text-grey-darker(type="date" placeholder="" v-model="IsDate" required )
                        div
                          label.block.text-grey-darker.text-sm.font-bold.mb-2 วันที่ครบกำหนด :
                          input.border.rounded.w-96.py-2.px-3.text-grey-darker(type="date" placeholder="" v-model="DueDate" required)
                  br
                  div.pl-4.space-x-4.pb-6.pt-3
                    button.btn.save.w-28.py-3.shadow-md.rounded-lg(type="submit") บันทึก
                    button.cancel.w-28.py-3.shadow-md.rounded-lg(type="submit" onclick="window.location.href='/Librarian/Loans'") ยกเลิก
      br
</template>

<script lang="js">
import { defineComponent } from '@nuxtjs/composition-api'
import axios from "axios"
import Vue from 'vue'
import vSelect from 'vue-select'
import Sidebar from '~/components/Librarian/Sidebar.vue'
import Navbar from '~/components/Librarian/EditMenu.vue'
import 'vue-select/dist/vue-select.css';
Vue.component('VSelect', vSelect)

export default defineComponent({
  components : {
    Sidebar,
    Navbar,
  },
  data() {
    return{
        bid:'',
        IDcard:'',
        IsDate:'',
        DueDate:'',
        books:[],
        lstatus:'กำลังดำเนินการ',
        status:'ไม่พร้อมใช้งาน',
    }
  },
  async fetch() {
    this.books = await fetch(
      'http://localhost:8080/books/'
    )
    .then((res) => res.json())
  },
  methods:{
    async formSubmit() {
      await axios.post('http://localhost:8080/loans/', {
        bid: this.bid,
        IDcard: this.IDcard,
        IsDate: this.IsDate,
        DueDate: this.DueDate,
        lstatus: this.lstatus,
      })
      .then(response => {
        console.log(response)
        alert("ดำเนินการเสร็จสิ้น...")
        axios.put(`http://localhost:8080/books/${this.bid}`, {
          status: this.status,
        })
        location.href='/Librarian/Loans'
      })
      .catch(err => {
        console.log(err)
        alert("เกิดข้อผิดพลาด...")
        location.href='/Librarian/Loans'
      })
    },
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

</style>