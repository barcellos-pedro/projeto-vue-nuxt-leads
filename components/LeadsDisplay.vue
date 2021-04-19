<template>
  <main class="leads">
    <div class="leads__search">
      <input
        type="text"
        class="search__input"
        placeholder="Search by name or bs"
      />
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      leads: [],
    }
  },
  async fetch() {
    this.leads = await fetch(
      'https://jsonplaceholder.typicode.com/users'
    ).then((response) => response.json())
  },
}
</script>

<style lang="scss" scoped>
.leads__search {
  width: 50%;
  margin: 0 auto;
  display: flex;
  justify-content: center;
}
.search__input {
  width: 14rem;
  height: 2rem;
  border: 1px solid $grey;
  border-radius: 4px;
  outline: none;
  transition: all 0.4s ease-in-out;
  padding: 0 1rem;
  &::placeholder {
    text-align: center;
  }
  &:hover {
    border: 1px solid $blue;
  }
  &:focus {
    box-shadow: 0 0 4px $blue;
  }
}
</style>
