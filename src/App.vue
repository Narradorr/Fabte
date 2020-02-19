<template>
  <div id="app">
    <TestHeader></TestHeader>
    <router-view></router-view>
    <div class="footer" style="background-color: #000; color: #fff; height: 50px; width: 100%;"></div>
  </div>
</template>

<script>
import TestHeader from "./components/Header.vue";
import TestSearch from "./components/Search.vue";
import ImageDetails from "./components/ImageDetails.vue";
import Favorites from "./components/Favorites.vue";

import Vue from "vue";
import VueResource from "vue-resource";
import VueRouter from 'vue-router'

Vue.use(VueRouter)
Vue.use(VueResource);

const routes = [
  { path: '/ImageDetails:id', name:'ImageDetails', component: ImageDetails },
  { path: '/search', component: TestSearch },
  { path: '/favorites', component: Favorites },
]
const router = new VueRouter({
  routes 
})

export default {
  router,
  name: "App",
  components: {
    TestHeader,
  },
  created: function() {
    router.replace({ path: 'search', redirect: '/' })
  }
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}


a,
a:active,
a:hover
{
  color: #fff;
  text-decoration: none;
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
 box-shadow: 0 14px 28px rgba(0,0,0,0.25), 0 10px 10px rgba(0,0,0,0.22);
}

.photos_item img {
  min-width: 100%;
  min-height: 100%;
}
</style>
