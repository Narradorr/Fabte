<template>
  <div v-if="photos" class="image_details_wrapper">
    <div class="photos_block">
      <div
        class="photos_item"
        v-for="photo in photos"
        v-bind:key="photo.id"
        v-bind:style="{ backgroundImage: 'url(' + photo.urls.regular + ')'}"
      >
        <router-link
          :to="{name: 'ImageDetails', params: {id: photo.id, photo: photo}}"
          style="width: 100%; height: 100%; display: block;"
        ></router-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "favorites",
  data: function() {
    return {
      photos: null
    };
  },
  methods: {},
  created: function() {
    this.photos = JSON.parse(localStorage.getItem("LocalPhotos"));
  }
};
</script>

<style scoped>
</style>