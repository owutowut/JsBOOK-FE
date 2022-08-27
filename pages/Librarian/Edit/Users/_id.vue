<template lang="pug">
  section.bg-silver
    Navbar
    div.flex
      Sidebar
      div.my-8.pt-4.pb-4.pl-8.bg-white.opacity-95.text-gray-800.w-full.h-full.mx-8.mt-6.rounded-xl
          .text-black.text-xl.font-bold ข้อมูลผู้ใช้
            div.mt-2
              hr
          .w-full.pl-6.pt-6.pr-12
              .container
                  form
                    div.grid-cols-3.flex.space-x-4
                      div
                        .mb-4
                          label.block.text-sm.font-bold.mb-2 รหัสหนังสือ :
                          input.border.rounded.w-96.py-2.px-3(type="text"  placeholder="" disabled="" v-model="id" )
                        .mb-4.flex.space-x-3
                          div
                            label.block.text-sm.font-bold.mb-2 ชื่อ :
                            input.border.rounded.py-2.px-3(type="text"  placeholder="" v-model="firstname" )
                          div
                            label.block.text-sm.font-bold.mb-2 นามสกุล :
                            input.border.rounded.py-2.px-3(type="text"  placeholder="" v-model="lastname" )
                        .mb-4
                          label.block.text-sm.font-bold.mb-2 เลขบัตรประชาชน :
                          input.border.rounded.py-2.px-3(type="text"  placeholder="" v-model="IDcard" )
                        .mb-4
                          label.block.text-sm.font-bold.mb-2 วันที่สร้างบัญชี :
                          p {{createDate}}
                        div.space-x-6.pb-6  
                          button.btn.save.w-28.py-3.mt-2.shadow-md.rounded-lg(type="submit" @click="update") บันทึก
                          button.cancel.w-28.py-3.mt-2.shadow-md.rounded-lg(type="submit" onclick="window.location.href='/Librarian/Users'") ยกเลิก
                      div.pl-5
                        .mb-4
                            label.block.text-sm.font-bold.mb-2 อีเมลล์ :
                            input.border.rounded.py-2.px-3(type="text"  placeholder="" v-model="email" )
                        .mb-4
                            label.block.text-sm.font-bold.mb-2 เบอร์โทรติดต่อ :
                            input.border.rounded.py-2.px-3(type="text"  placeholder="" v-model="tel" )
                        .mb-4
                            label.block.text-sm.font-bold.mb-4 บทบาทผู้ใช้ : {{role}}
                            select(v-model="role" class="text-center text-gray-800 rounded w-44 h-9 cursor-pointer border-2")
                              option member
                              option librarian
                      div.pl-5
                        .mb-4
                          label.block.text-lg รูปภาพ 
                          img.jpg.w-40.h-40(:src="img" alt="")      
</template>



<script lang="js">

import Vue from 'vue'
import axios from 'axios'
import Sidebar from '../../../../components/Librarian/Sidebar.vue'
import Navbar from '../../../../components/Librarian/EditMenu.vue'

export default Vue.extend({
  name: 'IndexPage',
  components : {
    Sidebar,
    Navbar
  },
   data() {
  return {
    id: '',
    firstname: '' ,
    lastname: '' ,
    IDcard: '',
    email: '' ,
    tel: '' ,
    createDate:'',
    img: '',
    role: '',
  }
  },
  
  async mounted() {
      const res = await axios.get(
        `http://localhost:8080/user/${this.$route.params.id}`
      )
      this.id=res.data._id
      this.firstname=res.data.firstname
      this.lastname=res.data.lastname
      this.email=res.data.email
      this.tel=res.data.tel
      this.IDcard=res.data.IDcard
      this.createDate=res.data.createDate
      this.img=res.data.img
      this.role=res.data.role
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
    },
    async update() {
      const res=await axios.put(`http://localhost:8080/user/${this.id}`, {
        role: this.role,
        firstname: this.firstname,
        lastname: this.lastname,
        IDcard: this.IDcard,
        email: this.email,
        tel: this.tel,
    })
    console.log(res.data)
    if(res.data) {
      alert('แก้ไขสำเร็จ')
      location.href='/Librarian/Users'
      }
    }
  },
})
</script >

<style scoped lang="scss">

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