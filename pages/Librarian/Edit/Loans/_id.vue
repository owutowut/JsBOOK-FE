<template lang="pug">
section.bg-silver.min-h-full
  Navbar
  div.flex
    Sidebar
    div.my-8.pt-8.pb-8.pl-8.bg-white.opacity-95.text-gray-800.w-full.h-full.mx-8.mt-6.rounded-xl
      div.space-y-3
        .text-black.text-xl.font-bold.pl-4 แก้ไขการยืม
          hr
        .w-full.pl-4.pt-2
            .container
                form.w-full
                  div.grid-cols-2.flex.space-x-14
                    div.space-y-4
                      div
                        label.block.text-sm.font-bold.mb-2 รหัสหนังสือ :
                        input.border.rounded.w-96.py-2.px-3(type="text"  placeholder=""  v-model="bid"  disabled="")
                      div
                        label.block.text-grey-darker.text-sm.font-bold.mb-3 เลขบัตรประชาชน :
                        input.border.rounded.w-96.py-2.px-3( type="text" v-model="IDcard"  disabled="")
                      div
                        label.block.text-grey-darker.text-sm.font-bold.mb-3 วันที่ยืม :
                        input.border.rounded.w-96.py-2.px-3( type="date" v-model="IsDate"  disabled="")
                    div.space-y-4
                      div
                        label.block.text-sm.font-bold.mb-2 วันครบกำหนด :
                        input.border.rounded.w-96.py-2.px-3(type="date" placeholder=""  v-model="DueDate"  disabled="")
                      div
                        label.block.text-sm.font-bold.mb-3 วันที่คืน :
                        input.border.rounded.w-96.py-2.px-3(type="date" v-model="ReDate")
                      div
                        label.block.text-sm.font-bold.mb-2 สถานะการยืม:
                        select.d.rounded-lg.border.px-4.py-3.w-80(v-model="lstatus")
                          option.py-1 กำลังดำเนินการ
                          option.py-1 เสร็จสิ้น
                          option.py-1 ล่าช้า
                br
                div.pl-4.space-x-6.pb-6  
                  button.btn.save.w-28.py-3.mt-2.shadow-md.rounded-lg(type="submit" @click="updateloans") บันทึก
                  button.cancel.w-28.py-3.mt-2.shadow-md.rounded-lg(type="submit" onclick="window.location.href='/Librarian/Loans'") ยกเลิก      
</template>

<script lang="js">

import Vue from 'vue'
import axios from "axios"
import Navbar from '../../../../components/Librarian/EditMenu.vue'
import Sidebar from '../../../../components/Librarian/Sidebar.vue'

export default Vue.extend({
  name: 'IndexPage',
  components : {
    Sidebar,
    Navbar,
  },
   data() {
  return {
    id:'',
    bid: '',
    lname: '' ,
    IsDate: '' ,
    IDcard:'',
    DueDate: '' ,
    ReDate: '' ,
    lstatus: '',
    status:'พร้อมใช้งาน',
  }
  },
  async fetch() {
      const res = await fetch(
        `http://localhost:8080/loans/${this.$route.params.id}`
      ).then((res) => res.json())
      this.id=res._id
      this.bid=res.bid
      this.lname=res.lname
      this.IsDate=res.IsDate
      this.DueDate=res.DueDate
      this.ReDate=res.ReDate
      this.lstatus=res.lstatus
      this.IDcard=res.IDcard
    },
  methods: {
    async updateloans() {
      const res=await axios.put(`http://localhost:8080/loans/${this.id}`, {
        bid: this.bid,
        lname: this.lname,
        IDcard: this.IDcard,
        IsDate: this.IsDate,
        DueDate: this.DueDate,
        lstatus: this.lstatus,
        ReDate: this.ReDate,
      })
    console.log(res.data)
    if(res.data) {
      alert('แก้ไขสำเร็จ')
      if(this.lstatus!=='กำลังดำเนินการ') { axios.put(`http://localhost:8080/books/${this.bid}`, {status: this.status,})}
      }
    location.href='/Librarian/Loans'
    }
  }
})
</script >

<style lang="postcss" scoped>
.btn {
    font-size: 16px;
    color: #fff;
    background-color: #409eff;
    border-color: #409eff;
    border-radius: 6px;
}
</style>