<template>
  <div>
    <div class="test-search">
      <input type="text" name="searchText" id="searchText" placeholder="Поиск" v-model="search" />
      <div class="search_btn" @click="onSearchFromUnsplash">
        <img src="../assets/search.svg" alt />
      </div>
    </div>
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
        this.getPhotos(this.currentPage + 1, this.search);
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
          localStorage.photos = this.photos;
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

.test-search input[type="text"] {
  width: 44%;
  padding: 20.5px 39px;
  font-family: SF UI Display;
  font-style: normal;
  font-weight: 300;
  font-size: 24px;
  line-height: 29px;
  color: #000000;
  border: none;
}

.search_btn {
  width: 70px;
  background-color: #fff;
  height: 70px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.search_btn:hover {
  background-color: #f4f4f4;
  cursor: pointer;
}

.photos_block {
  background-color: #f4f4f4;
  padding: 50px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.photos_item {
  padding: 3px;
  margin: 14px;
  width: 470px;
  height: 440px;
  overflow: hidden;
  background-size: cover;
  background-repeat: no-repeat;
  border-radius: 8px;
  box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
}

.photos_item img {
  min-width: 100%;
  min-height: 100%;
}

@media only screen and (max-width: 600px) {
  .test-search {
    padding: 0 18px;
  }

  .test-search input[type="text"] {
    width: 85%;
    padding: 20.5px;
  }

  .photos_block {
    padding: 20px;
  }

  .photos_item {
    padding: 0;
    margin-left: 0;
    margin-right: 0;
    margin-bottom: 7px;
    margin-top: 7px;
    width: 335.38px;
    height: 321.24px;
    box-shadow: none;
  }
}
</style>