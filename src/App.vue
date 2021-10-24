<template>
  <div class="main-layout">
    <calculator />
  </div>
</template>

<script>
import Calculator from "./components/Calculator.vue";

export default {
  name: "App",
  components: {
    Calculator,
  },
};
</script>

<style lang="scss">
.main-layout {
  width: 100vw;
  height: 100vh;
  background: $background-color;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
