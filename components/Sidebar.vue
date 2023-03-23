<template>
  <aside class="col-span-1 p-6 m-6 bg-gray-50 text-gray-800">
    <nav class="space-y-8 text-sm">
      <div class="space-y-2">
        <h2
          class="text-sm font-semibold tracking-widest uppercase text-gray-600"
        >
          Shares
        </h2>
        <Input />
        <div class="flex flex-col space-y-1">
		<Sidebar-share-tile
            v-for="(stock, i) in this.stocks"
            :key="i"
			:stock=stock
		 />
        </div>
      </div>
    </nav>
  </aside>
</template>
<script lang="ts">
module.exports = {
  props: {
	stocks: Array
	},
  data: function () {
    return {
      greeting: "Hello",
    };
  },
  methods: {
    fetchSuggestions() {},
  },
  mounted() {},
};
</script>
