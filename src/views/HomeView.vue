<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Places",
      places: [],
      currentPlace: {},
      newPlaceParams: {},
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
    createPlace: function () {
      console.log("Adding a new Place");
      axios
        .post("http://localhost:3000/places.json", this.newPlaceParams)
        .then((response) => {
          console.log("Place Added", response.data);
          this.places.push(response.data);
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <!-- Create New Place -->
    <h2>Input Info for New Place</h2>
    <div>
      Name:
      <input type="text" v-model="newPlaceParams.name" />
      Address:
      <input type="text" v-model="newPlaceParams.address" />
    </div>
    <button v-on:click="createPlace()">Add New Place</button>

    <!-- Index with Show Modal -->
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
