<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Places",
      places: [],
    };
  },
  created: function () {
    axios.get("http://localhost:3000/places.json").then((response) => {
      this.places = response.data;
      console.log("All Places", this.places);
    });
  },
  methods: {},
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>

    <div v-for="place in places" v-bind:key="place.id">
      <p>{{ place.name }}</p>
      <p>{{ place.address }}</p>
    </div>
  </div>
</template>

<style></style>
