<template>
  <div
    class="single-card-wrapper shadow-sm grid grid-cols-3 p-2 rounded-lg text-gray-800"
  >
    <div class="flex flex-col col-span-2 justify-center align-middle basis-9/12">
      <p class="text-3xl font-semibold leading-none">{{title}}</p>
    </div>
    <div class="col-span-1 m-auto">
        <div
        :style="{ background: color, transform: `rotate(${rotation}deg)` }"
        class="arrow_up  justify-center align-middle basis-3/12"
        ></div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    color: String,
    rotation: String,
    title: String
  },
};
</script>
<style>
.single-card-wrapper {
    background: #eae8e8;
    border: 1px solid #c9c9c9;
}

.arrow_up {
  width: 65px;
  height: 65px;
  -webkit-mask-image: url("~/assets/arrow.svg");
  mask-image: url("~/assets/arrow.svg");
  -webkit-mask-repeat: no-repeat;
  mask-repeat: no-repeat;
  background: green;
}
</style>