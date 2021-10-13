<template>
  <div class="loading" v-if="loading">
    <pulse-loader :loading="loading" color="#2c3e50" size="10px"></pulse-loader>
  </div>
</template>

<script>
import PulseLoader from "vue-spinner/src/PulseLoader.vue";

export default {
  name: "Loader",
  components: {
    PulseLoader,
  },
  props: {
    loading: Boolean,
  },
};
</script>

<style scoped>
.loading {
  position: fixed;
  width: 100vw;
  height: 100vh;
  z-index: 1500;
  background: #00000080;
  top: 0;
  left: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
