<template>
  <div>
    <div class="test-search">
      <input type="search" placeholder="Поиск" v-model="search" />
      <div
        style="
      width: 30px;
      height: 30px;
      background-color: red;
     "
        @click="onSearchFromUnsplash"
      ></div>
    </div>
    <div class="photos_block">
      <div
        class="photos_item"
        v-for="photo in photos"
        v-bind:key="photo.id"
        v-bind:style="{ backgroundImage: 'url(' + photo.urls.regular + ')'}"
      >
        <router-link :to="{name: 'ImageDetails', params: {id: photo.id, photo: photo}}" style="width: 100%; height: 100%; display: block;"></router-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "test-header",
  data() {
    return {
      search: "",
      bottom: false,
      photos: [],
      totalPhotos: 0,
      perPage: 9,
      currentPage: 1,
      w: 200
    };
  },
  watch: {
    bottom(bottom) {
      if (bottom) {
        this.getPhotos(this.currentPage + 1);
      }
    }
  },
  methods: {
    bottomVisible() {
      const scrollY = window.scrollY;
      const visible = document.documentElement.clientHeight;
      const pageHeight = document.documentElement.scrollHeight;
      const bottomOfPage = visible + scrollY >= pageHeight;
      return bottomOfPage || pageHeight < visible;
    },

    onSearchFromUnsplash: function() {
      this.photos = [];
      this.getPhotos(1, this.search);
    },
    getPhotos: function(page, searchQuery = "office") {
      var options = {
        params: {
          client_id: "2pHG11HZrvA1MEHqdJe8buRNVUxfCdgfBZrlnoCwigg",
          page: page,
          per_page: this.perPage,
          query: searchQuery
        }
      };

      console.log(searchQuery);

      this.$http
        .get("https://api.unsplash.com/search/photos", options)
        .then(function(response) {
          this.photos = this.photos.concat(response.data.results);
          localStorage.photos =   this.photos;
          this.totalPhotos = parseInt(response.headers.get("x-total"));
          this.currentPage = page;
        }, console.log);
    }
  },
  created: function() {
    window.addEventListener("scroll", () => {
      this.bottom = this.bottomVisible();
    });
    this.getPhotos(this.currentPage);
    localStorage.narradorid = 1;
    let narradorlocalid = localStorage.narradorid;
    console.log(narradorlocalid);
  }
};
</script>

<style >
.test-search {
  width: 100%;
  background: linear-gradient(0, rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)),
    url("../assets/search-background.jpg") #000;
  background-size: cover;
  background-repeat: no-repeat;
  background-position-y: 50%;
  height: 250px;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 0 200px;
  box-sizing: border-box;
  position: relative;
}

.test-search input[type="search"] {
  width: 44%;
  padding: 21px 39px;
  font-family: SF UI Display;
  font-style: normal;
  font-weight: 300;
  font-size: 24px;
  line-height: 29px;
  color: #000000;
}
</style>