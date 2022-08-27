<template lang="pug">
section.flex.flex-col.h-screen.items-center(class="md:flex-row")
  .bg-indigo-600.hidden.w-full.h-screen(class="lg:block md:w-1/2 xl:w-2/3")
    img.w-full.h-full.object-cover(src="https://theteethbeneath.files.wordpress.com/2015/02/beautiful-library-wallpaper-44313-45432-hd-wallpapers.jpg" alt="")

    
  .bg-white.w-full.h-screen.px-6.flex.items-center.justify-center(class="md:max-w-md lg:max-w-full md:mx-0 md:w-1/2 xl:w-1/3 lg:px-16 xl:px-12")
    .w-full.h-100
        h1.h.font-bold.leading-tight JAMIE's BOOK 

        h1.font-bold.leading-tight.mt-6(class="text-lg") Login to your account Member

        form.mt-6
            div
            label.block Email Address
            input.w-full.px-4.py-3.rounded-lg.mt-2.border(v-model="email" type="email" name="" id="" placeholder="Enter Email Address" class=" focus:bg-white " autofocus="" autocomplete="" required="")
        
        .mt-4
            label.block Password
            input.w-full.px-4.py-3.rounded-lg.mt-2.border(v-model="password" type="password" name="" id="" placeholder="Enter Password" minlength="6" maxlength="15" class=" focus:bg-white " required="")
        
        .flex.pt-4
          span(style="margin-right: 8px; margin-bottom: 8px;")
            span Sign in as: 
          .space-x-2
            button(type="button")
                nuxt-link.text-sm.text-red-main(:to="{ path: '/'}" class="text-blue-500 border-b border-blue ") Member
            a :
            button(type="button")
                nuxt-link.text-sm.text-red-main(:to="{ path: '/LibrarianAcc'}" class="text-blue-500 border-b border-blue ") Librarian



    
        .flex.justify-between.space-y-6.pt-1
            .flex.items-center
                input#remember_me.h-4.w-4.rounded(name="remember_me" type="checkbox")
                label.ml-2.block.text-sm.pb-1.font-semibold(for="remember_me") Remember
        
            .div.pb-5
                a.text-sm.font-semibold(href="#" )  Forgot Password
            
        button.login.w-full.block.font-semibold.rounded-lg.px-4.py-3.border.text-white.text-center(@click="login") Login 
            
        hr.my-6.w-full

        div.text-center
            a.font-semibold(href="/Register" ) Create an account 

</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      email: '',
      password: '',
    }
  },
  methods: {
    async login(){
      const res=await axios.post('http://localhost:8080/login',{
        email:this.email,
        password:this.password,
      })
      if(res.data==='invalid email or password') {
        alert('อีเมลหรือรหัสผ่านผิด กรุณาป้อนใหม่อีกครั้ง')
      }
      else{
        localStorage.setItem('token',res.data.token)
        alert('เข้าสู่ระบบสำเร็จ')
        this.$router.push('/Member/Main')
      }
      // console.log(res.data)
    }
  }
}
</script>

<style lang="postcss" scoped>
@import url('https://fonts.googleapis.com/css2?family=Rammetto+One&display=swap');

.login {
  background-color: #409eff;
}

.z {
    color: #409eff;
}

.h {
    color: #46614A;
    text-shadow: 2px 2px black;
    font-family: 'Rammetto One', cursive;
    font-size: 45px;
}


</style>
