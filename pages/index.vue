<template>
  <div class="leads">
    <h1 class="leads__title">Leads</h1>
    <leads-display />
  </div>
</template>

<script>
export default {}
</script>

<style lang="scss" scoped="true">
.leads {
  &__title {
    margin: 1.4rem 0;
    padding: 1.4rem 0;
    border-top: $border-color 1px solid;
  }
}
</style>
