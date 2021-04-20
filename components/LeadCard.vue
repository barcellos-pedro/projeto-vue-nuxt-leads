<template>
  <div class="lead">
    <p v-if="$fetchState.pending">Loading image...</p>
    <p v-else-if="$fetchState.error">An error occurred.</p>
    <div v-else>
      <img
        v-for="data in leadPicture.results"
        :key="data.login.uuid"
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
    lead: {
      type: Object,
      default: null,
    },
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
  margin: 1rem 0;
  display: grid;
  // grid-template-columns: 10% 16% 16% 16% 16% 16%;
  grid-template-columns: 8% 13% 26% 13% 13% 16%;
  grid-gap: 0 1rem;
  text-align: center;
  align-items: center;
  padding: 8px 16px;
  border: 1px solid #fff;
  transition: all 0.4s ease;
  @media (max-width: 767px) {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  &__image {
    border-radius: 100%;
  }
  &:hover {
    border: 1px solid $green;
    border-radius: 4px;
    img {
      border: 3px solid $green;
    }
  }
}
.lead__button {
  color: $dark-blue;
  transition: all 0.2s ease;
  &:hover {
    color: $light-blue;
  }
}
p {
  width: 100%;
}
img {
  border: 3px solid #fff;
  padding: 2px;
  transition: border 0.4s ease;
}
</style>
