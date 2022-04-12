<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Places",
      places: [],
      currentPlace: {},
    };
  },
  created: function () {
    axios.get("http://localhost:3000/places.json").then((response) => {
      this.places = response.data;
      console.log("All Places", this.places);
    });
  },
  methods: {
    showPlace: function (place) {
      console.log(place);
      this.currentPlace = place;
      document.querySelector("#place-details").showModal();
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>

    <div v-for="place in places" v-bind:key="place.id">
      <p>{{ place.name }}</p>
      <p>{{ place.address }}</p>
      <button v-on:click="showPlace(place)">More Info</button>
      <dialog id="place-details">
        <form method="dialog">
          <h1>Place Info</h1>
          <p>
            Name:
            <input type="text" v-model="currentPlace.name" />
          </p>
          <p>
            Address:
            <input type="text" v-model="currentPlace.address" />
          </p>
          <button>Close</button>
        </form>
      </dialog>
    </div>
  </div>
</template>

<style></style>
