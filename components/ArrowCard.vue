<template>
  <div
    class="single-card-wrapper shadow-sm grid grid-cols-3 p-3 rounded-lg text-gray-800"
  >
    <div class="flex flex-col col-span-2 justify-center align-middle basis-9/12">
      <p class="text-xl pl-3 font-semibold leading-none">{{title}}</p>
    </div>
    <div class="col-span-1 m-auto">
        <div
        :style="{ background: trend < 0 ? '#9FDC95' : '#F7BBB6', transform: `rotate(${trend}deg)` }"
        class="arrow_up  justify-center align-middle basis-3/12"
        ></div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    trendWeek: Number,
    trendYTD: Number,
    timePeriod: Boolean,
    title: String
  },
  computed: {
    trend() {
        let num = this.timePeriod ? this.trendYTD : this.trendWeek
        return ((num - -100) * (-90 - 90)) / (100 - -100) + 90;
    }
  },
  methods: {
    mapToRotation(num) {
      
    },
  }
};
</script>
<style>
.single-card-wrapper {
    cursor: pointer; 
    background: #eae8e8;
    border: 1px solid #c9c9c9;
}

.arrow_up {
  width: 45px;
  height: 45px;
  -webkit-mask-image: url("~/assets/arrow.svg");
  mask-image: url("~/assets/arrow.svg");
  -webkit-mask-repeat: no-repeat;
  mask-repeat: no-repeat;
  transition: all 0.5s ease-in-out;
}
</style>