<template>
  <div class="lead">
    <p v-if="$fetchState.pending">
      <loading-spinenr />
    </p>
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
  fetchDelay: 1000,
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
  grid-template-columns: 8% 13% 26% 13% 13% 16%;
  grid-gap: 0 1rem;
  text-align: center;
  align-items: center;
  padding: 8px 16px;
  border: 1px solid #fff;
  transition: all 0.4s ease;
  &::after {
    content: '';
    display: block;
    width: 90vw;
    border-bottom: 1px solid $border-color;
  }
  @media (max-width: 767px) {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  &:hover {
    border: 1px solid $green;
    border-radius: 4px;
    &::after {
      display: none;
    }
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
  border-radius: 100%;
  border: 3px solid #fff;
  padding: 2px;
  transition: border 0.4s ease;
}
</style>
