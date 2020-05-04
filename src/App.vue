<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <h1>{{ title }}</h1>
    <navbar />
    <allPhotos v-if="allPhotos" />
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
    /*
It should pause the Vue lifecycle by calling the created method. 
Read more about the Vue lifecycle here. 
Inside of that method, it should use the utility methods found in the utils/index.js file 
to make a call to Amazon's S3 service to retrieve 
a list of all items stored on the pre-specified S3 bucket.
*/
    getThings: function() {
      console.log("DOES THIS WORK???? inside getThings method of App.vue");
      console.log("this.photos INSIDE getThings(): ", this.photos);
      console.log("typeof this.photos: ", typeof this.photos);
      let photos = this.photos;
      // console.log("photos variable: ", photos);
      getImages();
      async function getImages() {
        let list = await listObjects();
        const baseSixtyFourArray = list.map(obj => {
          const key = obj.Key;
          return getSingleObject(key);
        });
        const arrayOfPhotosStrings = await Promise.all(baseSixtyFourArray);

        photos = arrayOfPhotosStrings;
        console.log("this is photos from at the END of async/await: ", photos);
      }
    },
    allPhotos: function() {
      // DO SOMETHING TO DISPLAY ALL PHOTOS
    },
    singlePhoto: function() {
      //Do something
    }
  },
  created() {
    this.getThings();
  },
  data: () => ({
    title: "Photo Upload App",
    currentView: "allPhotos",
    photos: [],
    selectedPhoto: ""
  })
};
</script>

<style>
#app {
  text-align: center;
}
</style>
