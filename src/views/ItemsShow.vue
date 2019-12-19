<template>
  <div class="items-show">
    <p>{{ item.name }}</p>
    <p>{{ item.price }}</p>
    <p>{{ item.description }}</p>
    <router-link to="/items">Back to all items</router-link> |
    <router-link v-bind:to="`/items/${item.id}/edit`">Edit item</router-link>
    <hr>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      item: {}
    };
  },
  created: function() {
    axios.get("/api/items/" + this.$route.params.id).then(response => {
      this.item = (response.data);
    });
  },
  methods: {}
};
</script>