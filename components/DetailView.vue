<template>
    <div class="detail-wrapper grid grid-cols-4" >
        <button class="bg-gray-500 hover:bg-gray-700 text-white font-bold py-2 px-4 rounded-full fixed top-10 right-20" @click="$emit('closeDetail')">x</button>
        <Sidebar :stocks=stocks />
        <div class="detail-content col-span-3 h-screen">
            
        </div>
    </div>
</template>
<script>
module.exports = {
  props: {
    stocks: Array
  },
}
</script>

<style>
    .detail-wrapper {
        width: 100vw;
        height: calc(100vh - 100px);
    }
    .detail-content {
        background: url('~/assets/mockscreen.png');
        height: 100%;
        background-size: contain;
        background-repeat: no-repeat;
        background-position: center;
    }
</style>