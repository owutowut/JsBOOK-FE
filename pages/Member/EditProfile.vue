<template lang="pug">
section.bg-silver.min-h-screen
  Navbar
  div.flex
    Sidebar
    div.my-8.pt-4.pb-4.pl-4.bg-white.opacity-95.text-gray-800.w-full.h-full.mx-8.mt-6.rounded-xl
      div.text-black.text-xl.font-bold.pl-6.pt-2 แก้ไขโปรไฟล์
        div.my-3
            hr
      div  
        br
      .h-full.px-6
        .border-b-2.block(class="md:flex")
          .w-full.p-4.bg-white.shadow-md(class="md:w-2/5 sm:p-6 lg:p-8 border")
            .flex.justify-between
              span.text-xl.font-semibold.block Edit Profile
            span.text-gray-600 Edit details about yourself
            .w-full.p-8.mx-2.flex.justify-center
          
              div(v-if="!image")
                label.flex.flex-col.rounded-lg.border-4.border-dashed.w-40.h-40.p-10.group.text-center
                  .h-full.w-full.text-center.flex.flex-col.items-center.justify-center
                      img.icon(src="https://cdn-icons-png.flaticon.com/512/568/568717.png")
                  input.hidden(type="file" @change="onFileChange" class="w-48 h-40 rounded-full ")
                  .w.text-black.border.rounded.font-semibold.cursor-pointer.p-1.px-3 Select
                
              div(v-else="")
                img(:src="image")
                button.t.px-4.py-2.border.rounded-md.font-semibold.text-xs.uppercase.tracking-widest.mt-2.ml-3.mr-4(@click="removeImage" class=" font-bold rounded")  delete
          

          .w-full.p-8.bg-white.shadow-md(class="md:w-3/5 lg:ml-4 border")
            .rounded.shadow.p-6
              .pb-6
                label.font-semibold.text-gray-700.block.pb-1 ชื่อ
                input.border.rounded-r.px-4.py-2.w-full(type="text" v-model="firstname")
              .pb-4
                label.font-semibold.text-gray-700.block.pb-1 นามสกุล
                input.border.rounded-r.px-4.py-2.w-full(type="text" v-model="lastname")
              .pb-4
                label.font-semibold.text-gray-700.block.pb-1 เบอร์โทรติดต่อ
                div.flex
                  span.text-sm.border.border-2.rounded-l.px-4.py-2.bg-gray-300 Tel
                  input.border.rounded-r.px-4.py-2.w-full(type="tel" name="phone" pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}" required=""  v-model="tel")

        .space-y-4.flex
          div(class="space-x-3")
            button.save.w-28.py-3.mt-6.shadow-lg.rounded-lg(type="submit" @click="submit"  ) บันทึก
            button.cancel.w-28.py-3.mt-6.shadow-lg.rounded-lg(type="submit" onclick="window.location.href='/Member/Loans'") ยกเลิก
        div  
          br
    </div>
  </div>
</template>

<script lang="js">

import Vue from 'vue'
import axios from 'axios'
import Sidebar from '../../components/Member/Sidebar.vue'
import Navbar from '../../components/Member/EditMenu.vue'

export default Vue.extend({
  name: 'IndexPage',
  components : {
    Sidebar,
    Navbar
  },
  data() {
    return {
      image: '',
      firstname: '',
      lastname: '',
      tel: '',
      cover: '',
      file:''
  }
  },
  async mounted() {
    const res=await axios.get('http://localhost:8080/profile', {
      headers: { authorization: `Bearer ${localStorage.getItem('token')}` },
    })
    this.firstname=res.data.firstname
    this.lastname=res.data.lastname
    this.tel=res.data.tel
  },

  methods: {
    onFileChange(e) {
      const files = e.target.files || e.dataTransfer.files;
      if (!files.length)
        return;
      this.createImage(files[0]);
      this.file=files[0]
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
     async submit() {
      const ref = this.$fire.storage.ref().child(`images/${this.file.name}`);
      await ref.put(this.file)
      const url = await ref.getDownloadURL()
      await axios.patch('http://localhost:8080/updateprofile',{
        firstname:this.firstname,
        lastname:this.lastname,
        tel:this.tel,
        img: url,
      },
      {
      headers: { authorization: `Bearer ${localStorage.getItem('token')}` },
    })
    alert( 'แก้ไขโปรไฟล์สำเร็จ' )
    location.reload()
    }
  }

})
</script>

<style scoped lang="scss">
.save {
  background-color: #409eff;
}
.cancel {
  background: #fff;
}

#app {
  text-align: center;
}

img {
  width: 155px;
  height: 155px;
  transition: transform 0.2s;
  &:hover {
    -ms-transform: scale(1.5); /* IE 9 */
    -webkit-transform: scale(1.5); /* Safari 3-8 */
    transform: scale(1.5);
  }
}

.icon {
  width: 30px;
  height: 30px;
}

.t:hover {
  background-color: #f56565;
  border-radius: 4px;
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

.w:hover {
  background-color: #409eff;
  border-radius: 4px;
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}
</style>
