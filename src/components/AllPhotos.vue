<template>
  <div class="mainDivAllPhotos">
    <div class="allPhotosDiv" v-for="photo in photos" :key="photo.id">
      <img @click="$emit('changeCurrentView')" class="allPhotos" :src="photo" alt="random" />
    </div>
  </div>
</template>

<script>
export default {
  name: "AllPhotos",
  props: ["photos"],
  methods: {
    switchToSinglePhoto: function() {
      // send clicked <img>'s src to SinglePhoto.vue
      // tell parent App.vue, that data.currentView = "singlePhoto"
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
