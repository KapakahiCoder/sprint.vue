<template>
  <div class="mainDivAllPhotos">
    <div class="allPhotosDiv" v-for="photo in photos" :key="photo.id">
      <img
        @click="changeCurrentView(); sendPhoto(photo);"
        class="allPhotos"
        :src="photo"
        alt="random"
      />
    </div>
  </div>
</template>



<script>
export default {
  name: "AllPhotos",
  props: ["photos"],
  methods: {
    sendPhoto: function(image) {
      console.log("INSIDE sendPhoto method");
      console.log("this is image: ", image);
      this.$emit("set-photo", image);
    },
    changeCurrentView: function() {
      this.$emit("changeCurrentView");
    }
  },
  data() {
    return { placeholderData: "placeholderData from AllPhotos.vue" };
  }
};
</script>

<style>
.allPhotos {
  width: 30%;
}
.allPhotosDiv {
  border: 1px solid grey;
  border-radius: 5px;
  padding: 25px;

  width: 30%;
}
</style>
