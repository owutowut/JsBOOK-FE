<template>
  <div class="relative">
    <button
      href="#"
      class="flex items-center"
      @click="toggleVisibility"
      @keydown.space.exact.prevent="toggleVisibility"
      @keydown.esc.exact="hideDropdown"
      @keydown.shift.tab="hideDropdown"
      @keydown.up.exact.prevent="startArrowKeys"
      @keydown.down.exact.prevent="startArrowKeys"
    >
      <img
        :src="profile.img"
        alt="avatar"
        class="mr-3 mt-1 w-9 h-9 rounded-full"
      />
      <div class="opacity-95 mt-1 flex items-center">
        <h1 class="text-white uppercase">
          {{ profile.firstname }} {{ profile.lastname }}
        </h1>
        <svg
          class="text-white pt-1"
          fill="currentColor"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
          width="30"
          height="30"
        >
          <path
            class="heroicon-ui"
            d="M15.3 9.3a1 1 0 0 1 1.4 1.4l-4 4a1 1 0 0 1-1.4 0l-4-4a1 1 0 0 1 1.4-1.4l3.3 3.29 3.3-3.3z"
          ></path>
        </svg>
      </div>
    </button>
    <transition name="dropdown-fade">
      <ul
        v-if="isVisible"
        ref="dropdown"
        v-on-clickaway="hideDropdown"
        class="
          absolute
          normal-case
          font-normal
          xs:left-0
          lg:right-0
          bg-white
          shadow
          overflow-hidden
          opacity-95
          rounded-md
          w-44
          border-2 border-green-navbar
          top-10
          mt-4
          lg:z-20
          text-green-text
        "
      >
        <li>
          <a
            ref="account"
            href="/Librarian/EditProfile"
            class="flex items-center px-4 py-3 hover:bg-silver"
            @keydown.up.exact.prevent=""
            @keydown.tab.exact="focusNext(false)"
            @keydown.down.exact.prevent="focusNext(true)"
            @keydown.esc.exact="hideDropdown"
          >
            <svg
              class="ml-2"
              fill="currentColor"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 24 24"
              width="26"
              height="26"
            >
              <path
                class="heroicon-ui"
                d="M12 12a5 5 0 1 1 0-10 5 5 0 0 1 0 10zm0-2a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm9 11a1 1 0 0 1-2 0v-2a3 3 0 0 0-3-3H8a3 3 0 0 0-3 3v2a1 1 0 0 1-2 0v-2a5 5 0 0 1 5-5h8a5 5 0 0 1 5 5v2z"
              ></path>
            </svg>
            <span class="ml-3">โปรไฟล์</span>
          </a>
        </li>
        <hr />
        <li>
          <a
            href="/Librarian/Loans"
            class="flex items-center px-4 py-3 hover:bg-silver"
            @keydown.tab.exact="focusNext(false)"
            @keydown.shift.tab="focusPrevious(false)"
            @keydown.up.exact.prevent="focusPrevious(true)"
            @keydown.down.exact.prevent="focusNext(true)"
            @keydown.esc.exact="hideDropdown"
          >
            <svg
              id="Capa_1"
              class="ml-2"
              width="25"
              height="25"
              fill="currentColor"
              xmlns="http://www.w3.org/2000/svg"
              xmlns:xlink="http://www.w3.org/1999/xlink"
              version="1.1"
              x="0px"
              y="0px"
              viewBox="0 0 490 490"
              style="enable-background: new 0 0 490 490"
              xml:space="preserve"
            >
              <path
                id="XMLID_1474_"
                d="M210,173.76c-9.484-6.35-20.592-9.757-32.224-9.756c-15.727,0-30.498,6.229-41.59,17.54  c-22.708,23.153-22.708,60.827,0,83.981l49.095,50.059c6.586,6.715,15.364,10.414,24.718,10.414s18.132-3.699,24.718-10.414  l49.096-50.06c22.708-23.154,22.708-60.827,0-83.981c-11.093-11.311-25.863-17.54-41.59-17.539  C230.591,164.003,219.482,167.411,210,173.76z M262.396,244.517l-49.097,50.061c-1.15,1.173-2.429,1.419-3.299,1.419  s-2.149-0.247-3.3-1.42l-49.096-50.06c-11.348-11.571-11.349-30.398,0-41.969v0c5.405-5.51,12.568-8.545,20.172-8.545  s14.768,3.035,20.178,8.552c0.297,0.303,0.584,0.613,0.866,0.926c1.994,2.215,5.493,4.963,11.488,4.963  c4.156,0,8.092-1.874,10.872-4.963c0.283-0.315,0.572-0.627,0.872-0.933c5.405-5.51,12.568-8.545,20.172-8.545  c7.604,0,14.768,3.035,20.172,8.545C273.744,214.12,273.744,232.947,262.396,244.517z M455,0H95C53.645,0,20,33.645,20,75v340  c0,41.355,33.645,75,75,75h360c8.284,0,15-6.716,15-15V15C470,6.716,463.284,0,455,0z M185,30h50v40.729l-18.292-9.146  C214.597,60.528,212.298,60,210,60s-4.597,0.528-6.708,1.583L185,70.729V30z M370,460H95c-24.813,0-45-20.187-45-45V75  c0-24.813,20.187-45,45-45h60v65c0,5.199,2.692,10.027,7.114,12.76c4.422,2.733,9.945,2.98,14.594,0.657L210,91.771l33.292,16.646  c4.649,2.324,10.17,2.077,14.594-0.657C262.308,105.027,265,100.199,265,95V30h105V460z M440,460h-40V30h40V460z"
              />
            </svg>
            <span class="ml-3">ระบบการยืม</span>
          </a>
        </li>
        <hr />
        <li>
          <a
            href="/"
            class="flex items-center px-2 py-3 hover:bg-silver"
            @keydown.tab.exact="focusNext(false)"
            @keydown.shift.tab="focusPrevious(false)"
            @keydown.up.exact.prevent="focusPrevious(true)"
            @keydown.down.exact.prevent="focusNext(true)"
            @keydown.esc.exact="hideDropdown"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="ml-5"
              width="26"
              height="26"
              x="0px"
              y="0px"
              fill="currentColor"
            >
              <path
                d="M16 10v-5l8 7-8 7v-5h-8v-4h8zm-16-8v20h14v-2h-12v-16h12v-2h-14z"
              />
            </svg>
            <span class="ml-2">ออกจากระบบ</span>
          </a>
        </li>
      </ul>
    </transition>
  </div>
</template>

<script>
import { mixin as clickaway } from 'vue-clickaway'
import axios from 'axios'

export default {
  mixins: [clickaway],
  data() {
    return {
      isVisible: false,
      focusedIndex: 0,
      profile: {},
    }
  },
  async mounted() {
    const res = await axios.get('http://localhost:8080/profile', {
      headers: { authorization: `Bearer ${localStorage.getItem('token')}` },
    })
    if (res.data === 'not have token') {
      location.href = '/loginLibrarian'
    } else {
      this.profile = res.data
    }
  },
  methods: {
    toggleVisibility() {
      this.isVisible = !this.isVisible
    },
    hideDropdown() {
      this.isVisible = false
      this.focusedIndex = 0
    },
    startArrowKeys() {
      if (this.isVisible) {
        // this.$refs.account.focus()
        this.$refs.dropdown.children[0].children[0].focus()
      }
    },
    focusPrevious(isArrowKey) {
      this.focusedIndex = this.focusedIndex - 1
      if (isArrowKey) {
        this.focusItem()
      }
    },
    focusNext(isArrowKey) {
      this.focusedIndex = this.focusedIndex + 1
      if (isArrowKey) {
        this.focusItem()
      }
    },
    focusItem() {
      this.$refs.dropdown.children[this.focusedIndex].children[0].focus()
    },
  },
}
</script>

<style scoped>
.dropdown-fade-enter-active,
.dropdown-fade-leave-active {
  transition: all 0.1s ease-in-out;
}

.dropdown-fade-enter,
.dropdown-fade-leave-to {
  opacity: 0;
  transform: translateY(-12px);
}

hr {
  width: 90%;
  margin-left: 5%;
}
</style>
