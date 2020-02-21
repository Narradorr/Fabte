<template>
  <div v-if="photo" class="image_details_wrapper">
    <div class="background_mask_block">
      <div class="background_mask_black_filter"></div>
      <div
        class="background_mask_img"
        v-bind:style="{ backgroundImage: 'url(' + photo.urls.regular + ')'}"
      ></div>
    </div>

    <div class="image_details_main_content">
      <div class="image_details_top_info">
        <div class="author_info_block">
          <div class="image_details_author_photo">
            <img :src="photo.user.profile_image.medium" alt />
          </div>
          <div class="author_name_block">
            <div>{{photo.user.name}}</div>
            <div class="dop_info">@{{photo.user.username}}</div>
          </div>
        </div>
        <div class="image_details_btns_block">
          <div class="favorite_btn" @click="ToLocalStorage">
            <img src="../assets/favorite.svg" alt />
          </div>
          <a :href="photo.urls.raw" download="FileName.jpg" class="download_image">
            <img src="../assets/download.svg" alt />
            <span class="download_text not_for_mobile">DOWNLOAD</span>
          </a>
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

          console.log(localPhotos.filter(e => e.id === this.photo.id).length);
          console.log(this.photo.Id);

          if (!localPhotos.filter(e => e.id === this.photo.id).length > 0) {
            localPhotos.push(this.photo);
            localStorage.LocalPhotos = JSON.stringify(localPhotos);
          }
        } else {
          let localPhotos = [];
          localPhotos.push(this.photo);
          localStorage.LocalPhotos = JSON.stringify(localPhotos);
        }
      }
      console.log("ToLocalStorage");
    }
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
  /* background-color: #000; */
  text-align: left;
}

.background_mask_block {
  width: 100%;
  height: 80%;
  position: absolute;
  overflow: hidden;
}

.background_mask_black_filter {
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
}

.background_mask_img {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1;
  filter: grayscale(1) blur(8px);
  /* filter: opacity(0.15); */
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
  padding: 46px 0 40px;
  color: #fff;
  display: flex;
  justify-content: space-between;
}

.image_details_main_content .image_details_photo {
  width: 100%;
  box-shadow: 0px 4px 50px rgba(0, 0, 0, 0.5);
  border-radius: 8px;
}

.author_info_block {
  display: flex;
}

.download_image,
.favorite_btn {
  height: 50px;
}

.download_image {
  background-color: #fff200;
  color: #000;
  display: inline-flex;
  line-height: 50px;
  padding: 0 20px;
  justify-content: space-between;
  border: 1px solid #fff200;
  box-sizing: border-box;
  box-shadow: 0px 0px 4px rgba(0, 0, 0, 0.25);
  border-radius: 8px;
}

.download_image:hover {
  background-color: #ffe600;
  cursor: pointer;
}

.download_image .download_text {
  font-family: Roboto;
  font-style: normal;
  font-weight: normal;
  font-size: 20px;
  line-height: 47px;
  color: #000000;
  margin-left: 16px;
}

.favorite_btn {
  background-color: #fff;
  color: #fff;
  padding: 15px;
  box-sizing: border-box;
  box-shadow: 0px 0px 4px rgba(0, 0, 0, 0.25);
  border-radius: 8px;
  margin-right: 20px;
}

.favorite_btn:hover {
  background-color: #f4f4f4;
  cursor: pointer;
}

.image_details_btns_block {
  display: flex;
}

.image_details_author_photo {
  margin-right: 10px;
}

.image_details_author_photo img {
  border-radius: 8px;
  width: 55px;
  height: 55px;
  border: 1px solid #fff;
  box-sizing: border-box;
}

.author_name_block {
  display: flex;
  flex-direction: column;
  padding: 10px 0;
  justify-content: space-between;
}

@media only screen and (max-width: 600px) {
  .author_name_block {
    display: flex;
    flex-direction: column;
    padding: 10px 0;
    justify-content: space-between;
  }
  .image_details_main_content {
    padding: 20px;
  }

  .download_image,
  .favorite_btn {
    height: 40px;
    line-height: 40px;
  }

  .favorite_btn {
    padding: 7px 10px;
  }

  .download_image {
    padding: 0 8.5px;
  }

  .favorite_btn img {
    width: 20px;
  }

  .background_mask_block {
    display: none;
  }

  .author_name_block {
    color: #000;
    font-size: 18px;
    justify-content: center;
    padding: 5px 0;
  }

  .image_details_author_photo img {
    border-radius: 8px;
    width: 48px;
    height: 48px;
  }

  .dop_info{
    color: #666;
    font-size: 14px;
  }

  .image_details_main_content .image_details_photo{
    box-shadow: none;
  }

  .image_details_main_content .image_details_top_info {
    padding: 40px 0 32px;
}
}
</style>