<template>
  <div class="items-index">
    <h1>{{ message }}</h1>

    Search: <input type="text" v-model="searchTerm" list="names">
    <datalist id="names">
      <option v-for="item in items"> {{ item.name }}</option>  
    </datalist>
    <br>
    <div v-for="item in filterBy(items, searchTerm, 'name')">
      <p>{{ item.name }}</p>
      <p>{{ item.price }}</p>
      <hr>
    </div>
    
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      items: {},
      searchTerm: ""
    };
  },
  created: function() {
    axios.get("/api/items").then(response => {
      this.items = (response.data);
    });
  },
  methods: {}
};
</script>