<template>
  <div class="test-header">
    <img alt="Test logo" src="../assets/logo.svg" />
    <div>
      <router-link class="header_link_item" to="search">Поиск</router-link>
      <router-link class="header_link_item" to="favorites">Избранное</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "test-header"
};
</script>

<style >
.test-header {
  width: 100%;
  background-color: #000;
  height: 148px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 200px;
  box-sizing: border-box;
  color: #fff;
}

.test-header .header_link_item{
  margin-right: 10px;
}
</style>