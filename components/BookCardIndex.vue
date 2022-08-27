<template>
    <div class="md:flex shadow-md py-4 px-6 bg-silver rounded-lg w-100% wrapper">
        <div class="md:flex-shrink-0 w-28 ml-2">
            <img 
                class="rounded-lg md:w-32" 
                :src="product.cover" 
                :alt="product.bname"
            />
        </div>
        <div class="grid-cols-3 flex space-x-3 ml-3 w-100%">
            <div class="mx-4 my-2 opacity-95 justify-start">
                <div class="tracking-wide text-lg font-bold opacity-90">
                    {{product.bname}}
                    <hr>
                </div>
                <div class="desbox grid-cols-2 space-y-1">
                    <div class="dbox">
                        <p class="text-gray-500 leading-relaxed text-sm mt-2 overflow-y-hidden font-medium"> 
                            {{product.description}}
                        </p>
                    </div>
                    <div class="sbox flex">
                        <p class="text-base font-semibold tracking-wide opacity-90 mt-1">
                            สถานะ :
                        </p>
                        <p class="text-base font-semibold tracking-wide opacity-90 mt-1 ml-2" :class="`${product.status=='ไม่พร้อมใช้งาน'?' text-red-700 ':' text-green-700 '}`">
                            {{product.status}}
                        </p>
                    </div>
                </div>
            </div>
            <div class="opacity-95 ibox">
                <div class="mt-8 space-y-2 ">
                    <div class="flex text-center ml-2">
                        <div class="w-20">
                            <p class="text-base font-bold">ผู้เขียน</p>
                        </div>
                        <div>
                            <p class="text-gray-500 leading-relaxed text-sm font-medium">{{product.author}}</p>
                        </div>
                    </div>
                    <div class="flex text-center ml-2">
                        <div class="w-20">
                            <p class="text-base font-bold">หมวดหมู่</p>
                        </div>
                        <div>
                            <p class="text-gray-500 leading-relaxed text-sm font-medium">{{product.category}}</p>
                        </div>
                    </div>
                    <div class="flex text-center ml-2">
                        <div class="w-20">
                            <p class="text-base font-bold">ปีที่พิมพ์</p>
                        </div>
                        <div>
                            <p class="text-gray-500 leading-relaxed text-sm font-medium">{{product.year}}</p>
                        </div>
                    </div>
                </div>
            </div>
            <div class="cbox my-3 text-center">
                <div class="ml-4">
                    <p class="tracking-wide text-lg font-bold opacity-90">เนื้อหา</p>
                    <p class="text-gray-500 leading-relaxed text-sm font-medium">{{product.content}}</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        product: {
            type: Object,
            default: () => {}
        }
    }
}
</script>

<style scoped>
.desbox{
    width: 450px;
}

.dbox{
    height: 75px;
}

.sbox{
    width: 200px;
}

.cbox{
    width: 480px;
    height: 130px;
    overflow-y: auto;
}

.ibox{
    width: 300px;
}

.wrapper{
  max-height: 300px;
  overflow-x: auto;
  overflow-y: hidden;
}

.wrapper::-webkit-scrollbar{
  width: 0;
  height: 12px;
}

.wrapper .item{
  line-height: 300px;
  text-align: center;
  background-color: #ddd;
}

.wrapper::-webkit-scrollbar:hover {
  background-color: lightslategray;
}
</style>