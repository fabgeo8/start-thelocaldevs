<template>
  <transition mode="out-in">
    <div
      class="sidebar-share-tile"
      :class="{ 'sidebar-share-tile--expanded': isExpanded }"
      @click="isExpanded = !isExpanded"
    >
      <div class="sidebar-share-tile__title">
        <input
          type="radio"
          value=""
          name="default-radio"
          class="default-radio-1 w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600"
        />
        {{ stock.name }}
      </div>
      <div class="sidebar-share-tile__trend">{{ stock.trend }}</div>
      <div v-show="isExpanded" class="sidebar-share-tile__description">
        {{ stock.description }}
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  props: {
    stock: Object,
  },
  data: function () {
    return {
      isExpanded: false,
    };
  },
};
</script>

<style>
.sidebar-share-tile {
  background-color: #dddddd;
  border-radius: 4px;
  padding: 5px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  transition: height 0.2s ease-in;
}

.sidebar-share-tile__description {
  flex: 0 0 100%;
}

.default-radio-1 {
  margin-right: 5px;
}

.sidebar-share-tile__title {
  height: 100%;
  display: flex;
  align-items: center;
}
.sidebar-share-tile__trend {
  height: 100%;
}
</style>