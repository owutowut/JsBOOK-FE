<template >
  <div class="side min-h-screen">
    <div class="opacity-95 w-44 bg-white border-r h-full">
      <div>
        <ul class="pt-3 py-2 space-y-2 font-extrabold text-lg text-gray-800">
          <li>
            <a href="/Librarian/Users" class="relative flex flex-row items-center h-11 border-l-4 border-transparent  pr-6 hover:bg-jame  ">
              <span class="inline-flex justify-center items-center ml-8 w-6 h-6 rounded-lg">
                  <img src="https://www.svgrepo.com/show/39996/user.svg" alt="">
              </span>
              <span class="ml-4 text-base font-semibold">ผู้ใช้</span>
            </a>
          </li>
          <div class="px-3">
            <hr>
          </div>
          <li>
            <a
              href="/Librarian/Loans"
              class="relative flex flex-row items-center h-11 border-l-4 border-transparent  pr-6 hover:bg-jame "
            >
              <span class="inline-flex justify-center items-center ml-8 w-6 h-6 rounded-lg">
                  <img src="https://cdn-icons-png.flaticon.com/512/4221/4221578.png" alt="">
              </span>
              <span class="ml-4 text-base font-semibold">การยืม</span>
            </a>
          </li>
          <div class="px-3">
            <hr>
          </div>
          <li>
            <a
              href="/Librarian/Books"
              class="jame relative flex flex-row items-center h-11 border-l-4 border-transparent hover:bg-jame "
            >
              <span class="inline-flex justify-center items-center ml-8 w-6 h-6 rounded-lg ">
                  <img src="https://www.svgrepo.com/show/12094/book.svg" alt="">
              </span>
              <span class="ml-4 text-base font-semibold">หนังสือ</span>
            </a>
          </li>
          <div class="px-3">
            <hr>
          </div>
        </ul>
      </div>
    </div>
  </div>
</template>