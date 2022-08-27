<template lang="pug">
.bg-slate-800.bg-opacity-50.flex.justify-center.items-center.absolute.top-0.right-0.bottom-0.left-0
  .bg-white.px-16.py-14.rounded-md.text-center.border
    h1.text-xl.mb-4.font-bold.text-slate-500 Do you Want Delete
    button.bg-indigo-500.px-4.py-2.rounded-md.text-md.text-white Cancle
    button.bg-red-500.px-7.py-2.ml-2.rounded-md.text-md.text-white.font-semibold Ok
    
    .items-center.pt-3.grid.grid-cols-2.gap-y-6.rounded.border.mr-6
        div.flex.pl-4.pt-5
          label.block.w-24 ชื่อผู้ใช้งาน
          input.d.rounded-lg.border.px-4.py-3.w-96(placeholder="ชื่อผู้ใช้งาน" class=" focus:bg-white")
        div.flex.pt-5
          label.block.w-28 วันที่สร้างบัญชี
          input.d.rounded-lg.border.px-4.py-3.w-96(placeholder="ว/ด/ป" class=" focus:bg-white" type="date")
        div.flex.pl-4
          label.block.w-24 อีเมลล์
          input.d.rounded-lg.border.px-4.py-3.w-96(placeholder="Email Address" class=" focus:bg-white" )
        div.flex.pl-4
          label.block.w-24 บทบาท
          select.d.rounded-lg.border.px-4.py-3.w-96
            option.py-1 --
            option.py-1 Librarian
            option.py-1 Member
</template>
