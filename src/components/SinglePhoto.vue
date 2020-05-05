<template>
  <div>
    <img class="selectedPhoto" :src="selectedPhoto" alt="random" />
  </div>
</template>

<script>
export default {
  name: "SinglePhoto",
  props: ["selectedPhoto"],
  methods: {
    onClickButton(event) {
      this.$emit("clicked", "singlePhotos");
    }
  }
};
</script>

<style></style>
