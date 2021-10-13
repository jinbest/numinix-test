<template>
  <div class="header"></div>
</template>

<script>
export default {
  name: "Header",
};
</script>

<style scoped>
.header {
  width: 100%;
  height: 90px;
  position: fixed;
  z-index: 1000;
  top: 0;
  left: 0;
  background: #fff;
  box-shadow: 9px 6px 24px -2px #00000060;
}
@media (max-width: 600px) {
  .header {
    height: 65px;
  }
}
</style>
