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

* {
  box-sizing: border-box;
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

</style>
