<template>
  <section class="h-screen card-container p-6">
    <div
      class="container  grid grid-cols-1 gap-6 mx-auto sm:grid-cols-3 xl:grid-cols-4"
      @click="$emit('shareSelected')"
    >
      <ArrowCard
        v-for="(stock, i) in stocks"
        :key="i"
        :title="stock.name"
        :color="stock.trendYTD > 0 ? '#9FDC95' : '#F7BBB6'"
        :rotation="'' + mapToRotation(stock.trendYTD)"
      />
    </div>
  </section>
</template>
<script>
module.exports = {
  props: {
    stocks: Array
  },
  data: () => {
    return {
    };
  },
  methods: {
    mapToRotation(num) {
      return ((num - -100) * (-90 - 90)) / (100 - -100) + 90;
    },
  },
};
</script>
<style>
.card-container {
  background: #fff;
}
</style>

