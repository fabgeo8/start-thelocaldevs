<template>
    <div class="detail-wrapper grid grid-cols-4" >
        <!-- <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full fixed top-140 right-20" @click="$emit('closeDetail')">x</button> -->
        <Sidebar :stocks=stocks />
        <div class="detail-content col-span-3 h-screen">
            <!-- <div class="flex justify-center content-center h-screen">
                <iframe style="border: 1px solid rgba(0, 0, 0, 0.1);" width="800" height="450" src="https://www.figma.com/embed?embed_host=share&url=https%3A%2F%2Fwww.figma.com%2Fproto%2FzBN0TOXDpjyZyK1Z8EWJW2%2FSTART-Hack%3Fnode-id%3D20-2%26scaling%3Dscale-down%26page-id%3D0%253A1%26starting-point-node-id%3D20%253A2" allowfullscreen></iframe>
            </div> -->
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