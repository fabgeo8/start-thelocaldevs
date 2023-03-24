<template>
  <header class="p-4 bg-gray-100 text-gray-800">
    <div class="container flex justify-between h-16 mx-auto">
      <!-- <ul class="items-stretch hidden space-x-3 lg:flex">
        <li class="flex">
          <a
            rel="noopener noreferrer"
            href="#"
            class="flex items-center px-4 -mb-1 border-b-2 border-transparent text-teal-600 border-teal-600"
            >Home</a
          >
        </li>
        <li class="flex">
          <a
            rel="noopener noreferrer"
            href="#"
            class="flex items-center px-4 -mb-1 border-b-2 border-transparent"
            >Finance</a
          >
        </li>
        <li class="flex">
          <a
            rel="noopener noreferrer"
            href="#"
            class="flex items-center px-4 -mb-1 border-b-2 border-transparent"
            >Stocks</a
          >
        </li>
      </ul> -->
      <a
        rel="noopener noreferrer"
        href="#"
        aria-label="Back to homepage"
        class="flex items-center p-2"
      >
        <img class="logo" src="~/assets/SIX_Logo.png" alt="" srcset="">
      </a>
      <div class="flex items-center md:space-x-4">
        <Input />
      </div>
      <button title="Open menu" type="button" class="p-4 lg:hidden">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
          class="w-6 h-6 text-gray-800"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M4 6h16M4 12h16M4 18h16"
          ></path>
        </svg>
      </button>
    </div>
  </header>
</template>
<script>
module.exports = {
  data: function () {
    return {
      greeting: "Hello",
    };
  },
  methods: {
    fetchSuggestions() {
        console.log("fetch");

    }
  },
  mounted() {
  }
};
</script>
<style>
.logo {
    width: 200px;
}
</style>

