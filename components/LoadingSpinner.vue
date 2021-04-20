<template>
  <span class="circle"></span>
</template>

<script>
export default {}
</script>

<style lang="scss" scoped>
.circle {
  animation: is-rotating 1s infinite;
  border: 6px solid #e5e5e5;
  border-radius: 50%;
  border-top-color: $blue;
  height: 50px;
  width: 50px;
}
@keyframes is-rotating {
  to {
    transform: rotate(1turn);
  }
}
</style>
