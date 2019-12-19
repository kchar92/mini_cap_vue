<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="item in items">
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
export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      items: {}
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
