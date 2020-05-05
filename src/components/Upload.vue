<template>
  <div>
    <button @click="triggerInput">
      <input type="file" class="input" style="display: none;" @click="uploadPhoto" />
      Upload!
    </button>
  </div>
</template>

<script>
export default {
  name: "Upload",
  methods: {
    triggerInput: function() {
      // MAKE THE INPUT WORK
    },
    uploadPhoto: function() {
      // use saveObject() from utils
    }
  }
};
</script>

<style>
</style>
