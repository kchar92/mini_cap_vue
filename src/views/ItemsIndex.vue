<template>
  <div class="items-index">
    <h1>{{ message }}</h1>

    Search: <input type="text" v-model="searchTerm" list="names">
    <datalist id="names">
      <option v-for="item in items"> {{ item.name }}</option>  
    </datalist>
    <br>
    <div v-for="item in filterBy(items, searchTerm, 'name')" v-bind:class="{selected: item.selected}">
      <button v-on:click="selectItem(item)">Select Item</button>
      <p>{{ item.id }}</p>
      <p>{{ item.name }}</p>
      <p>{{ item.price }}</p>
      <router-link v-bind:to="`/items/${item.id}`">Go to the show page</router-link>
      <hr>
    </div>
    
  </div>
</template>

<style>
.selected {
  color: white;
  background-color: steelBlue;
  transition: background-color 1s ease;
}
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
      // console.log(response.data);
      this.items = (response.data);
    });
  },
  methods: {
    selectItem: function(item) {
      console.log("item selected");
      item.selected = !item.selected;
      console.log(item);
    }
  }
};
</script>