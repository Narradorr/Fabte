<template>
  <div class="test-header">
    <img class="test_logo" alt="Test logo" src="../assets/logo.svg" />
    <div class="links_block">
      <router-link class="header_link_item" to="search">
        <img src="../assets/search_white.svg" alt />
        <span class="menu_item_text not_for_mobile">Поиск</span>
      </router-link>
      <router-link class="header_link_item" to="favorites">
        <img src="../assets/favorite_white.svg" alt />
        <span class="menu_item_text not_for_mobile">Избранное</span>
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "test-header"
};
</script>

<style >
.links_block a:last-child {
  margin-right: 0;
}
.test-header {
  width: 100%;
  background-color: #000;
  height: 140px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 200px;
  box-sizing: border-box;
  color: #fff;
}

.test-header .header_link_item {
  margin-right: 40px;
  justify-content: center;
  display: inline-flex;
}

.menu_item_text {
  font-family: Roboto;
  font-style: normal;
  font-weight: normal;
  font-size: 18px;
  line-height: 23px;
  margin-left: 9px;
}

@media only screen and (max-width: 600px) {
  .test-header {
    padding: 0 5%;
    height: 80px;
  }

  .test-header .test_logo {
    width: 84px;
  }

  .not_for_mobile {
    display: none;
  }
}
</style>