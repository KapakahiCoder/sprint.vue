<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <h1>{{ title }}</h1>
    <navbar />
    <allPhotos v-if="currentView==='allPhotos'" />
    <singlePhoto v-else />
  </div>
</template>

<script>
import Navbar from "./components/Navbar";
import AllPhotos from "./components/AllPhotos";
import SinglePhoto from "./components/SinglePhoto";
import { listObjects, getSingleObject } from "../utils/index.js";

console.log("IS THIS WORKING????? Inside <script> of App.vue");
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
    }
  },
  created() {
    //  console.log("inside created()");
    function getPhotos() {
      listObjects()
        .then(data => {
          console.log("this is data: ", data);
          let arrayOfObjs = data;
          console.log("this is arrayOfObjs BEFORE map: ", arrayOfObjs);
          arrayOfObjs = arrayOfObjs.map(obj => {
            console.log("this is obj.Key", obj.Key);
            return getSingleObject(obj.Key);
          });
          console.log("this is arrayOfObjs AFTER map:", arrayOfObjs);
          let longStrings = Promise.all(arrayOfObjs);
          console.log("this is longStrings", longStrings);
          return longStrings;
        })
        .then(result => {
          //  console.log("inside Promise.all().getSingleObject().then()");
          // console.log("THIS IS res: ", res);
          console.log("this is this.photos BEFORE reassigning:", this.photos);
          console.log("this is result", result);
          this.photos = result;
          console.log("this.photos AFTER reassigning", this.photos);
        });
    }
    getPhotos();
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
