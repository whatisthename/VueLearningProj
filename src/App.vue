<template>
  <div id="app">
    <!-- <img src="./assets/logo.png"> -->
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
#app {
  width: 100vw;           /* 视口宽度 */
  height: 100vh;          /* 视口高度 */
  margin: 0;
  padding: 0;
  overflow: hidden;       /* 如果内容超过屏幕，可以设置为scroll来滚动查看 */
  position: fixed;        /* 固定定位 */
  top: 0;
  left: 0;
}
</style>
