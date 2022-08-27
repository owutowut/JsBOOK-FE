<template lang="pug">
section.bg-silver.min-h-screen
  Navbar
  div.flex
    Sidebar
    div.my-8.pt-4.pb-4.pl-4.bg-white.opacity-95.text-gray-800.w-full.h-full.mx-8.mt-6.rounded-xl
        div.text-black.text-xl.font-bold.pl-6.pt-2 ข้อมูลหนังสือ
        div.my-3
            hr
        .w-full.pl-8.pr-12(class="h-full")
            .container.pt-3
                div.grid-cols-2.flex.space-x-16
                    div.space-y-6
                      div
                        label.block.text-sm.font-bold.mb-2 รหัสหนังสือ :
                        p.ml-2 {{id}}
                      div
                        label.block.text-sm.font-bold.mb-2 ชื่อหนังสือ :
                        p.ml-2 {{bname}}
                      div
                        label.block.text-sm.font-bold.mb-2 ผู้เขียน :
                        p.ml-2 {{author}}
                      div
                        label.block.text-sm.font-bold.mb-2 หมวดหมู่ :
                        p.ml-2 {{category}}
                      div
                        label.block.text-sm.font-bold.mb-2 สถานะ :
                        p.ml-2(:class="`${status=='ไม่พร้อมใช้งาน'?' text-red-700 ':' text-green-700 '}`") {{status}}
                    div.space-y-6
                      div
                        label.block.text-sm.font-bold.mb-2 คำอธิบาย :
                        p.ml-2 {{description}}
                      div
                        label.block.text-sm.font-bold.mb-2.overflow-x-auto สื่อ :
                        p.ml-2 {{content}}
                      div
                        label.block.text-sm.font-bold.mb-2 ปกหนังสือ
                          div.mt-2.ml-2
                            img.jpg.w-full.h-full(:src="cover" alt="")
        div
          br
</template>



<script lang="js">

import Vue from 'vue'
import Sidebar from '../../../../components/Member/Sidebar.vue'
import Navbar from '../../../../components/Member/EditMenu.vue'

export default Vue.extend({
  name: 'IndexPage',
  components : {
    Sidebar,
    Navbar
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
    rating: '' ,
    status: '',
    cover: '',
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
      this.rating=res.rating
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
      // const image = new Image();
      const reader = new FileReader();
      const vm = this;

      reader.onload = (e) => {
        vm.image = e.target.result;
      };
      reader.readAsDataURL(file);
    },
    removeImage () {
      this.image = '';
    }
  }
  

})
</script >

<style scoped lang="scss">

img {
  width: 150px;
  height: 200px;
  transition: transform .2s;
  &:hover {
  -ms-transform: scale(1.5); /* IE 9 */
  -webkit-transform: scale(1.5); /* Safari 3-8 */
  transform: scale(1.5); 
  }
}

.icon {
  width: 40px;
  height: 40px;
}

.t:hover {
  background-color: #f56565;
  border-radius: 4px;
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

.w:hover {
  background-color: rgb(136, 132, 132);
  border-radius: 4px;
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

.save {
  background-color: #409eff;
  border: 1px solid #dcdfe6;
  &:hover {
  background-color: #b3d8ff;
  }
}

.cancel {
  background: #fff;
  border: 1px solid #dcdfe6;
}

</style>