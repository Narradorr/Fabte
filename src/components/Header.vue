<template>
  <div class="test-header">
    <img alt="Test logo" src="../assets/logo.svg" />
    <div>
      <router-link to="search">Поиск</router-link>
      <router-link to="favorites">Избранное</router-link>
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
}
</style>