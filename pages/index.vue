<template>
  <div>
    <Header />
    <Sidebar />
  </div>
</template>

<script lang="ts">
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
