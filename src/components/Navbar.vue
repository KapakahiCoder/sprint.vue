<template>
  <div>
    <a href="#" @click="allPhotos">Home</a>
    <upload />
  </div>
</template>

<script>
import Upload from "./Upload";

export default {
  name: "Navbar",
  methods: {
    allPhotos: function() {
      // DO SOMETHING TO CHANGE VIEW
      // TO ALL PHOTOS
    }
  },
  components: {
    upload: Upload
  }
};
</script>

<style></style>
