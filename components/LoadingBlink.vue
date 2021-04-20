<template>
  <div class="blink"></div>
</template>

<script>
export default {}
</script>

<style lang="scss" scoped>
@keyframes blinker {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
.blink {
  width: 25px;
  height: 25px;
  background-color: light($secondary, 10%);
  border-radius: 100%;
  display: block;
  animation: 0.6s ease-in-out infinite alternate blinker;
}
</style>
