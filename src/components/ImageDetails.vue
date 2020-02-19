<template>
  <div v-if="photo" class="image_details_wrapper">
    <div
      class="background_mask"
      v-bind:style="{ backgroundImage: 'url(' + photo.urls.regular + ')'}"
    ></div>

    <div class="image_details_main_content">
      <div class="image_details_top_info">
        <div class="author_info_block">
          <div>
            <img :src="photo.user.profile_image.medium" alt />
          </div>
          <div class="author_name_block">
            <div>{{photo.user.name}}</div>
            <div>@{{photo.user.username}}</div>
          </div>
        </div>
        <div>
          <div
            style="width: 40px;height: 40px;background-color: #333;color: #fff;"
            @click="ToLocalStorage"
          >LIKE</div>
          <a :href="photo.urls.raw" download="FileName.jpg">DOWNLOAD </a>
        </div>
      </div>
      <img class="image_details_photo" :src="photo.urls.regular" alt />
    </div>
  </div>
</template>

<script>
export default {
  name: "image-details",
  data: function() {
    return {
      id: null,
      photo: null
    };
  },
  methods: {
    ToLocalStorage: function() {
      if (this.photo) {
        if (localStorage.getItem("LocalPhotos")) {
          let localPhotos = JSON.parse(localStorage.getItem("LocalPhotos"));
          localPhotos.push(this.photo);
          localStorage.LocalPhotos = JSON.stringify(localPhotos);
        } else {
          let localPhotos = [];
          localPhotos.push(this.photo);
          localStorage.LocalPhotos = JSON.stringify(localPhotos);
        }
      }
      console.log("ToLocalStorage");
    },
  },
  created: function() {
    let idd = this.$route.params.id;
    let photo = this.$route.params.photo;
    console.log(photo);
    this.id = idd;
    this.photo = photo;
  }
};
</script>

<style scoped>
.image_details_wrapper {
  width: 100%;
  position: relative;
  background-color: #000;
  text-align: left;
}

.background_mask {
  width: 100%;
  height: 80%;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1;
  filter: grayscale(1);
  filter: opacity(0.15);
  background-repeat: no-repeat;
  background-size: cover;
}

.image_details_main_content {
  z-index: 2;
  position: relative;
  padding: 0 15%;
}

.image_details_main_content .image_details_top_info {
  width: 100%;
  padding: 20px 0;
  color: #fff;
  display: flex;
  justify-content: space-between;
}

.image_details_main_content .image_details_photo {
  width: 100%;
}

.author_info_block{
  display: flex;
}
</style>