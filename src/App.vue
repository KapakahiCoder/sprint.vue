<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <h1>{{ title }}</h1>
    <navbar />
    <allPhotos
      v-if="currentView==='allPhotos'"
      :photos="photos"
      v-on:changeCurrentView="currentView='singlePhoto'"
    />
    <singlePhoto v-else :selectedPhoto="selectedPhoto" />
  </div>
</template>

<script>
import Navbar from "./components/Navbar";
import AllPhotos from "./components/AllPhotos";
import SinglePhoto from "./components/SinglePhoto";
import { listObjects, getSingleObject } from "../utils/index.js";

export default {
  name: "App",
  components: {
    navbar: Navbar,
    allPhotos: AllPhotos,
    singlePhoto: SinglePhoto
  },
  methods: {
    currentViewFunc: function(updateCurrentViewString) {
      this.currentView = updateCurrentViewString;
    },
    getPhotos: function() {
      listObjects()
        .then(data => {
          let arrayOfObjs = data;
          arrayOfObjs = arrayOfObjs.map(obj => {
            return getSingleObject(obj.Key);
          });
          let longStrings = Promise.all(arrayOfObjs);
          return longStrings;
        })
        .then(result => {
          let baseSixtyFourArr = result.map(strings => {
            return `data:image/jpg;base64, ${strings}`;
          });
          return Promise.all(baseSixtyFourArr);
        })
        .then(longStrings => {
          this.photos = longStrings;
        });
    }
  },
  async created() {
    await this.getPhotos();
  },
  data: function() {
    return {
      title: "Photo Upload App",
      currentView: "allPhotos",
      photos: [],
      selectedPhoto: ""
    };
  }
};
</script>

<style>
#app {
  text-align: center;
}
</style>
