<template>
  <div>
    <Header />
    <section class="h-screen card-container p-6">
      <div class="switch-container flex justify-center items-center p-2 my-3">
        <span class="mx-2">Trend Year</span>
        <label class="switch">
          <input type="checkbox" @click="toggleCheckbox" />
          <div class="slider round"></div>
        </label>
        <span class="mx-2">Trend Week</span>
      </div>
      <div v-if="errorMessage !== ''" class="error flex justify-center">
        <div
          class="bg-red-100 border border-red-400 text-red-700 px-4 py-3 rounded relative w-full sm:w-1/2"
          role="alert"
        >
          <strong class="font-bold">An error occured:</strong>
          <span class="block sm:inline">{{ errorMessage }}</span>
        </div>
      </div>
      <div
        class="container grid grid-cols-1 gap-6 mx-auto sm:grid-cols-3 xl:grid-cols-4"
        @click="$emit('shareSelected')"
      >
        <ArrowCard
          v-for="(stock, i) in stocks"
          :key="i"
          :title="stock.name"
          :trendYTD="stock.trendYTD"
          :trendWeek="stock.trend7"
          :timePeriod="timePeriod"
        />
      </div>
    </section>
  </div>
</template>
<script>
module.exports = {
  props: {
    stocks: Array,
    errorMessage: String
  },
  data: () => {
    return {
      timePeriod: true,
    };
  },
  methods: {
    toggleCheckbox() {
      this.timePeriod = !this.timePeriod;
      this.$emit("setCheckboxVal", this.timePeriod);
    },
  },
};
</script>
<style>
.card-container {
  background: #fff;
}
.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
}

.switch input {
  display: none;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

input:checked + .slider {
  background-color: #101010;
}

input:focus + .slider {
  box-shadow: 0 0 1px #101010;
}

input:checked + .slider:before {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(26px);
}

.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}
</style>

