<template>
<div>
  <input
    v-model="inputValue"
    @keyup="fetchSuggestions"
    type="search"
    name="Search"
    placeholder="Search..."
    class="w-32 py-2 pl-10 text-sm rounded-md sm:w-auto focus:outline-none bg-gray-100 text-gray-800 focus:bg-gray-50"
  />
    <div v-show="suggestions.length > 0 && inputValue !== ''" class="suggestions w-32 py-2 pl-10 text-sm rounded-md">
        <div v-for="(s,i)  in suggestions" :key="i" class="single-suggestion">
            {{s.hit.name}}
        </div>
    </div>
</div>
</template>
<style lang="postcss" scoped>
    .suggestions {
        background: grey;
        position: absolute;
        max-height: 150px;
        width: 100%;
        z-index: 5;
        overflow: scroll;
    }
</style>
<script lang="ts">
module.exports = {
  data: function () {
    return {
      inputValue: "",
      suggestions: []
    };
  },
  methods: {
    fetchSuggestions() {
      console.log("fetch", this.inputValue);
      let uri = "https://web.api.six-group.com/api/findata/v1/searchInstruments?query=" + this.inputValue;
      fetch (uri, {
            method: "GET",
            mode: "cors",
            cache: "no-cache",
            credentials: "same-origin",
            headers: {
            "api-version": "2023-01-01",
            "Accept-Encoding": "gzip",
            "Accept": "application/json"
            }
        })
        .then((response) => response.json())
        .then((data) => {
            this.suggestions = data.data.searchInstruments.filter(el => el.hit.instrumentType == "EQUITY");
            console.log(data.data);
            
        }); 
    },
  },
  mounted() {},
};
</script>

