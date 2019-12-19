<template>
  <div class="items-edit">
    <h1>{{ message }}</h1>
    <div class="container">
      <form v-on:submit.prevent="editItem(item)">
        <h1>Edit Item: {{ item.name }}</h1>
        <ul>
          <li class="text-danger" v-for="error in errors">{{ error }}</li>
        </ul>
        <div class="form-group">
          <label>Name:</label> 
          <input type="text" class="form-control" v-model="item.ItemName">
        </div>
        <div class="form-group">
          <label>Price:</label>
          <input type="text" class="form-control" v-model="item.ItemPrice">
        </div>
        <div class="form-group">
          <label>Description:</label>
          <input type="text" class="form-control" v-model="item.ItemDescription">
        </div>
        <input type="submit" class="btn btn-primary" value="Submit">
      </form>
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
      message: "The edit page!",
      item: {},
      errors: []
    };
  },
  created: function() {
    axios.get("/api/items/" + this.$route.params.id).then(response => {
      this.item = response.data;
    });
  },
  methods: {
    editItem: function(item) {
      var params = {
        name: item.ItemName,
        price: item.ItemPrice,
        description: item.ItemDescription
      };
      axios.patch("/api/items/" + item.id, params).then(response => {
        this.$router.push("/items");
      })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    }
  }
};
</script>