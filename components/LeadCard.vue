<template>
  <div class="lead">
    <div v-for="data in leadPicture.results" :key="data.id">
      <img
        :src="data.picture.thumbnail"
        alt="lead picture"
        class="lead__image"
      />
    </div>
    <NuxtLink to="/" class="lead__button">{{ lead.name }}</NuxtLink>
    <p>{{ lead.email }}</p>
    <p>{{ lead.company.name }}</p>
    <p>{{ lead.phone }}</p>
    <p>{{ lead.company.bs }}</p>
  </div>
</template>

<script>
export default {
  props: {
    lead: Object,
  },
  data() {
    return {
      leadPicture: [],
    }
  },
  async fetch() {
    this.leadPicture = await fetch(
      'https://randomuser.me/api/?results=1'
    ).then((response) => response.json())
  },
}
</script>

<style lang="scss" scoped>
.lead {
  padding: 0 1rem;
  margin-top: 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  &__image {
    border-radius: 100%;
  }
  &__button {
    color: $dark-blue;
    transition: all 0.2s ease-in-out;
    &:hover {
      color: $light-blue;
    }
  }
}
</style>
