<template>
  <div>
    <Header />
    <Sidebar />
  </div>
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
