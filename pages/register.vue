<template>
  <div class="my-8 grid min-h-screen place-items-center">
    <div class="w-11/12 p-12 bg-white  lg:w-4/12 border ">
      <h1 class=" h text-xl font-semibold ">
        สมัครสมาชิก 
      </h1>
      <form class="้mt-6" @submit.prevent="register">
        <div class="flex justify-between gap-3 pt-4">
          <span class="w-1/2 ">
            <label
              for="firstname"
              class="ml-2 block text-xs font-semibold text-gray-600 uppercase"
              >ชื่อจริง</label
            >
            <input
              id="firstname"
              v-model="firstname"
              type="text"
              name="firstname"
              placeholder="John"
              autocomplete="given-name"
              pattern="[^0-9]*" title="ชื่อจริงต้องไม่มีตัวเลข"
              class="block w-full p-3 mt-2 text-gray-700 bg-gray-200 appearance-none focus:outline-none focus:bg-gray-300 focus:shadow-inner"
              required
            />
          </span>

          <span class="w-1/2">
            <label
              for="lastname"
              class="ml-2 block text-xs font-semibold text-gray-600 uppercase"
              >นามสกุล</label
            >
            <input
              id="lastname"
              v-model="lastname"
              type="text"
              name="lastname"
              placeholder="Doe"
              pattern="[^0-9]*" title="นามสกุลต้องไม่มีตัวเลข"
              autocomplete="family-name"
              class="block w-full p-3 mt-2 text-gray-700 bg-gray-200 appearance-none focus:outline-none focus:bg-gray-300 focus:shadow-inner"
              required
            />
          </span>
        </div>

        <label
          for="IDcard"
          class="ml-2 block mt-2 text-xs font-semibold text-gray-600 uppercase"
        >เลขบัตรประชาชน</label
        >
        <input
          id="IDcard"
          v-model="IDcard"
          type="text"
          name="IDcard"
          maxlength="13"
          placeholder="0000000000000"
          pattern="[0-9]{13}" title="กรุณาป้อนเลขบัตรประชาชน 13 หลัก"
          class="block w-full p-3 mt-2 text-gray-700 bg-gray-200 appearance-none focus:outline-none focus:bg-gray-300 focus:shadow-inner"
          required
        />

        <label
          for="email"
          class="ml-2 block mt-2 text-xs font-semibold text-gray-600 uppercase"
          >อีเมล</label
        >
        <input
          id="email"
          v-model="email"
          type="email"
          name="email"
          placeholder="john.doe@company.com"
          autocomplete="email"
          pattern="[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,}$" title="กรุณาป้อนอีเมลใหม่อีกครั้ง"
          class="block w-full p-3 mt-2 text-gray-700 bg-gray-200 appearance-none focus:outline-none focus:bg-gray-300 focus:shadow-inner"
          required
        />

        <label
          for="tel"
          class="ml-2 block mt-2 text-xs font-semibold text-gray-600 uppercase"
          >เบอร์โทรติดต่อ</label
        >
        <input
          id="Tel"
          v-model="tel"
          type="tel"
          name="tel"
          placeholder="0123456789"
          pattern="[0-9]{10}" title="กรุณาป้อนเบอร์โทรติดต่อใหม่อีกครั้ง"
          autocomplete="tel"
          class="block w-full p-3 mt-2 text-gray-700 bg-gray-200 appearance-none focus:outline-none focus:bg-gray-300 focus:shadow-inner"
          required
        />


        <label
          for="password"
          class="ml-2 block mt-2 text-xs font-semibold text-gray-600 uppercase"
          >รหัสผ่าน</label
        >
        <input
          id="password"
          v-model="password"
          type="password"
          name="password"
          placeholder="********"
          autocomplete="new-password"
          pattern=".{8,}" title="กรุณาป้อนรหัสผ่าน 8 ตัวขึ้นไป"
          class="block w-full p-3 mt-2 text-gray-700 bg-gray-200 appearance-none focus:outline-none focus:bg-gray-300 focus:shadow-inner"
          required
        />


        <label
          for="password-confirm"
          class="ml-2 block mt-2 text-xs font-semibold text-gray-600 uppercase"
          >ยืนยันรหัสผ่าน</label
        >
        <input
          id="password-confirm"
          type="password"
          name="password-confirm"
          placeholder="********"
          autocomplete="new-password"
          pattern=".{8,}" title="กรุณาป้อนรหัสผ่าน 8 ตัวขึ้นไป"
          class="block w-full p-3 mt-2 text-gray-700 bg-gray-200 appearance-none focus:outline-none focus:bg-gray-300 focus:shadow-inner"
          required
        />

        
        <button
          type="submit"
          class="w-full py-3 mt-6 font-medium tracking-widest text-white uppercase bg-blue-500 shadow-lg focus:outline-none hover:bg-blue-400 hover:shadow-none"
        >
          Sign up
        </button>

        <div class="text-gray-600 mt-6 pl-20">
            Already have an account ? 
            <a class="no-underline border-b border-blue text-blue-500" href="../">
                Log in
            </a>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      firstname: '' ,
      lastname: '',
      email: '',
      tel: '',
      password: '',
      IDcard:'',
    }
  },
  methods: {
    async register(){
      const res=await axios.post('http://localhost:8080/user',{
        firstname:this.firstname,
        lastname:this.lastname,
        email:this.email,
        tel:this.tel,
        password:this.password,
        IDcard:this.IDcard,
      })
      if(res.data==='email is used') {
        alert('อีเมลนี้ลงทะเบียนแล้ว')
      }
      else{
        alert('สมัครสมาชิกเสร็จสิ้น')
        this.$router.push('/')
      }
    }
  }
}
</script>
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Rammetto+One&display=swap');
</style>