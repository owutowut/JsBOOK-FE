<template lang="pug">
section.bg-silver
  Navbar
  div.flex
    Sidebar
    div.my-8.pt-8.pb-8.pl-8.bg-white.opacity-95.text-gray-800.w-full.h-full.mx-8.mt-6.rounded-xl
      div.space-y-3
        .text-black.text-xl.font-bold.pl-4 แก้ไขหนังสือ
        hr
        .w-full.pl-4.pt-2
            .container
                form
                  div.grid-cols-3.flex.space-x-14
                    div.space-y-4
                      div
                        label.block.text-sm.font-bold.mb-2 รหัสหนังสือ :
                        input.border.rounded.w-96.py-2.px-3(type="text"  placeholder="" disabled="" v-model="id" )
                      div
                        label.block.text-sm.font-bold.mb-2 ชื่อหนังสือ :
                        input.border.rounded.w-96.py-2.px-3(type="text"  placeholder=""  v-model="bname")
                      div
                        label.block.text-sm.font-bold.mb-2 ผู้เขียน :
                        input.border.rounded.w-96.py-2.px-3(type="text"  placeholder="" v-model="author" )
                      div
                        label.block.text-grey-darker.text-sm.font-bold.mb-3 คำอธิบาย :
                        textarea.border.rounded.w-96.py-2.px-3(rows="6" cols="50" v-model="description")
                    div.space-y-4
                      div
                        label.block.text-sm.font-bold.mb-2 หมวดหมู่ :
                        input.border.rounded.w-96.py-2.px-3(type="text"  placeholder=""  v-model="category")
                      div
                        label.block.text-sm.font-bold.mb-3 เนื้อหา :
                        textarea.border.rounded.w-96.py-2.px-3(rows="6" cols="50"  v-model="content")
                      div
                        label.block.text-sm.font-bold.mb-2 สถานะ :
                        select.d.rounded-lg.border.px-4.py-3.w-80(v-model="status")
                          option.py-1 พร้อมใช้งาน
                          option.py-1 ไม่พร้อมใช้งาน
                          
                    div.space-y-4    
                      div(class="md:flex-shrink-0 w-28 mx-12 mt-4")
                        div(class="rounded-lg md:w-28")
                          img.jpg.w-full.h-full(:src="cover" alt="")
                      div
                        label.block.mt-2.mb-2.text-lg.text-gray-600(for="tel") ปกหนังสือ 
                        input(type="file" @change="onFileSelected")
                        
                div.pl-4.space-x-4.pb-6  
                  button.btn.save.w-28.py-3.mt-6.shadow-md.rounded-lg(type="submit" @click="updatebooks") บันทึก
                  button.cancel.w-28.py-3.mt-6.shadow-md.rounded-lg(type="submit" onclick="window.location.href='/Librarian/Books'") ยกเลิก
                  
</template>

<script lang="js">

import Vue from 'vue'
import axios from "axios"
import Sidebar from '../../../../components/Librarian/Sidebar.vue'
import Navbar from '../../../../components/Librarian/EditMenu.vue'

export default Vue.extend({
  name: 'IndexPage',
  components : {
    Navbar,
    Sidebar,
  },
  data() {
    return {
      id: '',
      image: '' ,
      bname: '' ,
      author: '' ,
      description: '' ,
      category: '' ,
      content: '' ,
      status: '',
      cover:'',
  }
  },
  async fetch() {
      const res = await fetch(
        `http://localhost:8080/books/${this.$route.params.id}`
      ).then((res) => res.json())
      this.id=res._id
      this.bname=res.bname
      this.author=res.author
      this.description=res.description
      this.category=res.category
      this.content=res.content
      this.status=res.status
      this.cover=res.cover
    },

  methods: {
    onFileChange(e) {
      const files = e.target.files || e.dataTransfer.files;
      if (!files.length)
        return;
      this.createImage(files[0]);
    },
    createImage(file) {
      const reader = new FileReader();
      const vm = this;

      reader.onload = (e) => {
        vm.image = e.target.result;
      };
      reader.readAsDataURL(file);
    },
    removeImage () {
      this.image = '';
    },
    async updatebooks() {
      const res=await axios.put(`http://localhost:8080/books/${this.id}`, {
        bname: this.bname,
        author: this.author,
        description: this.description,
        content: this.content,
        category: this.category,
        cover: this.cover,
        status: this.status,
    })
    console.log(res.data)
    if(res.data) {
      alert('แก้ไขสำเร็จ')
      // this.$router.push('/Admin/books')
      location.href='/Librarian/Books'
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
</style>
