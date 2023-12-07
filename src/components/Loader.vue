<template>
  <div>
    <div class="loader" v-show="loading">
      <div class="lds-ring">
        <div></div>
        <div></div>
        <div></div>
        <div></div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
defineProps({ loading: Boolean });
</script>

<style scoped lang="scss">
.loader {
  width: 100%;
  height: 100vh;
  background: rgba($color: #000000, $alpha: 0.8);
  position: fixed;
  top: 0;
  left: 0;
  z-index: 999999999999999999 !important;
  display: grid;
  place-content: center;
}

// loader

.lds-ring {
  display: inline-block;
  position: relative;
  width: 60px;
  height: 60px;
}
.lds-ring div {
  box-sizing: border-box;
  display: block;
  position: absolute;
  width: 44px;
  height: 44px;
  margin: 8px;
  border: 4px solid #fff;
  border-radius: 50%;
  animation: lds-ring 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
  border-color: #fff transparent transparent transparent;
}
.lds-ring div:nth-child(1) {
  animation-delay: -0.45s;
}
.lds-ring div:nth-child(2) {
  animation-delay: -0.3s;
}
.lds-ring div:nth-child(3) {
  animation-delay: -0.15s;
}
@keyframes lds-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
