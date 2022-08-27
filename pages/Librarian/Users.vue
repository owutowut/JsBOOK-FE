<template lang="pug">
section.bg-silver
  Navbar
  div.flex
    Sidebar
    div.my-8.pt-8.pb-4.pl-8.bg-white.opacity-95.text-gray-800.w-full.h-full.mx-8.mt-6.rounded
      h1.font-semibold.text-2xl.pl-4 สมาชิก
      div.mt-2
        hr
      div.flex.space-x-2.mt-4 
        input.rounded-lg.border.px-2.py-2.w-80(placeholder="ค้นหาด้วยเลขบัตรประชาชน . . . " class=" focus:bg-white" v-model="searchName")
      
      .pt-4.mr-6
        table.w-full.rounded-lg
          thead
            tr.border
              th.px-5.py-3.text-left.text-xs.font-semibold.uppercase.tracking-wider.border.text-center  รูปโปรไฟล์
              th.px-5.py-3.text-left.text-xs.font-semibold.uppercase.tracking-wider.border.text-center  อีเมลล์
              th.px-5.py-3.text-left.text-xs.font-semibold.uppercase.tracking-wider.border.text-center  ชื่อผู้ใช้งาน
              th.px-5.py-3.text-left.text-xs.font-semibold.uppercase.tracking-wider.border.text-center  บทบาท
              th.px-5.py-3.text-left.text-xs.font-semibold.uppercase.tracking-wider.border.text-center  วันที่สมัครสมาชิก
              th.px-5.py-3.text-left.text-xs.font-semibold.uppercase.tracking-wider.border.text-center  จัดการข้อมูล
          tbody
            tr(v-for="(user, index) in filtered" :key="index")

              td.px-5.py-5.border.text-sm
                .flex.items-center
                  .flex.w-20.h-20
                    img.w-full.h-full.rounded-lg(:src="user.img")
                    
              td.px-5.py-5.border.text-sm.text-center
                p {{user.email}}

              td.px-5.py-5.border.text-sm.text-center 
                p {{user.firstname}} {{user.lastname}}

              td.px-5.py-5.border.text-sm.text-center 
                p {{user.role}}
              
              td.px-5.py-5.border.text-sm.font-semibold.text-center 
                p {{user.createDate}}
              
              td.px-5.py-5.border.text-sm.border-r
                .flex.space-x-3.pl-6
                  a.text-center(:href="`/Librarian/Edit/Users/${user._id}` " title="title" class="text-blue-500") Edit
                  button(class="text-red-500" @click="deleteuser(user._id)") Delete

</template>

<script lang="js">
import axios from 'axios'
import Sidebar from '../../components/Librarian/Sidebar.vue'
import Navbar from '../../components/Librarian/EditMenu.vue'
export default {
  name: 'IndexPage',
  components : {
    Sidebar,
    Navbar,
  },
  data() {
    return {
      users: [],
      searchName: '',
    }
  },
  computed:{
    filtered(){
      if(this.searchName) {
        return this.users.filter((user) => user.IDcard.match(this.searchName));
      }
      else{
        return this.users
      }
      },
    
    },
  async mounted() {
    const res=await axios.get('http://localhost:8080/user')
    this.users=res.data
    // console.log(res.data)
  },
  methods: {
    async deleteuser(id) {
    if(confirm(`คุณต้องการลบข้อมูลนี้หรือไม่`)) {
    await axios.delete(`http://localhost:8080/user/${id}`)
      location.reload()
    }},
  },
}
</script>

<style scoped>
.z {
  font-size: 16px;
  color: #fff;
  background-color: #409eff;
  border-color: #409eff;
  border-radius: 6px;
}

.reset {
  font-size: 16px;
  color: black;
  background-color: white;
  border-color: black;
  border-radius: 6px;
}

.enter {
  font-size: 16px;
  color: #fff;
  background-color: #409eff;
  border-color: #409eff;
  border-radius: 6px;
}

.tablebox {
  height: 460px;
}
</style>
