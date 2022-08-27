<template lang="pug">
section.bg-silver.h-full
  Navbar
  div.flex
    Sidebar
    div.my-8.pt-8.pb-4.bg-white.opacity-95.text-gray-800.w-full.h-full.mx-8.mt-6.rounded-xl
      div.space-y-3
          .text-black.text-xl.font-bold.pl-4 เพิ่มหนังสือ
          hr
          div.pl-14.pt-2
            form(@submit.prevent="formSubmit")
              div
                div.grid-cols-3.flex.space-x-14
                  div.space-y-3
                    div
                        label.block.text-sm.font-bold.mb-3 ชื่อหนังสือ :
                        input.border.rounded.w-96.py-2.px-3(type="text" placeholder="" v-model="bname" required)
                    div
                        label.block.text-sm.font-bold.mb-3 ผู้เขียน :
                        input.border.rounded.w-96.py-2.px-3(type="text" placeholder="" v-model="author" required)

                    div
                        label.block.text-grey-darker.text-sm.font-bold.mb-3 คำอธิบาย :
                        textarea.border.rounded.w-96.py-2.px-3(rows="6" cols="50" v-model="description" required)                        
                  div.space-y-3
                    div
                        label.block.text-sm.font-bold.mb-3 หมวดหมู่ :
                        input.border.rounded.w-96.py-2.px-3(type="text" placeholder="" v-model="category" required)            
                    div
                        label.block.text-sm.font-bold.mb-3 ปีที่พิมพ์ :
                        input.border.rounded.w-96.py-2.px-3(type="text" placeholder="" v-model="year" required)  
                    div
                        label.block.text-sm.font-bold.mb-3 เนื้อหา :
                        textarea.border.rounded.w-96.py-2.px-3(rows="6" cols="50"  v-model="content" required)
                  div.space-y-3
                      div
                        label.block.text-sm.font-bold.mb-3 สถานะ :
                        select(v-model="status" required class="text-center text-gray-800 rounded w-64 h-10 cursor-pointer border-2")
                          option(disabled, value) เลือกสถานะ
                          option พร้อมใช้งาน
                          option ไม่พร้อมใช้งาน
                      br              
                      label.block.mt-2.mb-2.text-lg.text-gray-600(for="tel") ปกหนังสือ 
                      input(type="file" @change="onFileSelected")
              div.pl-4.space-x-4.pb-6.pt-3
                button.btn.save.w-28.py-3.shadow-md.rounded-lg(type="submit") บันทึก
                button.cancel.w-28.py-3.shadow-md.rounded-lg(type="submit" onclick="window.location.href='/Librarian/Books'") ยกเลิก
      br
</template>

<script lang="js">
import { defineComponent } from '@nuxtjs/composition-api'
import axios from "axios"
import Sidebar from '../../../components/Librarian/Sidebar.vue'
import Navbar from '../../../components/Librarian/EditMenu.vue'

export default defineComponent({
  components : {
    Sidebar,
    Navbar,
  },
  data() {
    return{
        bname:'',
        year:'',
        author:'',
        description:'',
        content:'',
        category:'',
        cover:'',
        status:'พร้อมใช้งาน',
    }
  },
  methods:{
    onFileSelected(event) {
      this.selectedFile = event.target.files[0]
    },
    async formSubmit() {
      const ref = this.$fire.storage.ref().child(`images/${this.selectedFile.name}`);
      await ref.put(this.selectedFile)
      const url = await ref.getDownloadURL()
      await axios.post('http://localhost:8080/books/', {
        bname: this.bname,
        year: this.year,
        author: this.author,
        description: this.description,
        content: this.content,
        category: this.category,
        cover: url,
        status: this.status,
      })
      .then(response => {
        console.log(response)
        alert("ดำเนินการเสร็จสิ้น")
        location.href='/Librarian/Books'
      })
      .catch(err => {
        console.log(err)
        alert("เกิดข้อผิดพลาด")
        location.href='/Librarian/Books'
      })
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
</style>
