<template>
  <div class="items-new">
    <h1>{{ message }}</h1>
    <div class="container">
      <form v-on:submit.prevent="createItem()">
        <h1>Create Item</h1>
        <ul>
          <li class="text-danger" v-for="error in errors">{{ error }}</li>
        </ul>
        <div class="form-group">
          <label>Name:</label> 
          <input type="text" class="form-control" v-model="ItemName">
        </div>
        <div class="form-group">
          <label>Price:</label>
          <input type="text" class="form-control" v-model="ItemPrice">
        </div>
        <div class="form-group">
          <label>Description:</label>
          <input type="text" class="form-control" v-model="ItemDescription">
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
      message: "Welcome to the index!",
      ItemName: "",
      ItemPrice: "",
      ItemDescription: "",
      errors: []
    };
  },
  created: function() {},
  methods: {
    createItem: function() {
      var params = {
        name: this.ItemName,
        price: this.ItemPrice,
        description: this.ItemDescription
      };
      axios.post("/api/items", params).then(response => {
        this.$router.push("/items");
      })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    }
  }
};
</script>
