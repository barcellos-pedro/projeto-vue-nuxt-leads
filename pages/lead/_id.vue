<template>
  <div class="lead">
    <div v-if="$fetchState.pending" class="lead__pending">Fetching lead...</div>
    <div v-else-if="$fetchState.error" class="lead__error">
      An error occurred :(
    </div>
    <div v-else class="lead__fetched">
      <div class="data">
        <div class="data__header">
          <img
            v-for="user in image.results"
            :key="user.login.uuid"
            :src="user.picture.thumbnail"
            alt="lead picture"
          />
          <h3 class="data__name">{{ lead.name }}</h3>
        </div>
        <div class="data__body">
          <section class="data__summary">
            <div class="data__chunk">
              <div class="chunk__group">
                <p>{{ lead.username }}</p>
                <p>User</p>
              </div>
              <div class="chunk__group">
                <p>{{ lead.email }}</p>
                <p>E-mail</p>
              </div>
              <div class="chunk__group">
                <p>{{ lead.phone }}</p>
                <p>Phone</p>
              </div>
              <div class="chunk__group">
                <p>{{ lead.website }}</p>
                <p>Website</p>
              </div>
            </div>
          </section>
          <section class="data__relation">
            <h4>Company</h4>
            <div class="data__chunk">
              <div class="chunk__group">
                <p>{{ lead.company.name }}</p>
                <p>Name</p>
              </div>
              <div class="chunk__group">
                <p>{{ lead.company.catchPhrase }}</p>
                <p>Catch Phrase</p>
              </div>
              <div class="chunk__group">
                <p>{{ lead.company.bs }}</p>
                <p>BS</p>
              </div>
            </div>
          </section>
          <section class="data__relation">
            <h4>Address</h4>
            <div class="data__chunk">
              <div class="chunk__group">
                <p>{{ lead.address.city }}</p>
                <p>City</p>
              </div>
              <div class="chunk__group">
                <p>{{ lead.address.street }}</p>
                <p>Street</p>
              </div>
              <div class="chunk__group">
                <p>{{ lead.address.suite }}</p>
                <p>Suite</p>
              </div>
              <div class="chunk__group">
                <p>{{ lead.address.zipcode }}</p>
                <p>Zipcode</p>
              </div>
              <div class="chunk__group">
                <p>{{ lead.address.geo.lat }}</p>
                <p>Lat</p>
              </div>
              <div class="chunk__group">
                <p>{{ lead.address.geo.lng }}</p>
                <p>Long</p>
              </div>
            </div>
          </section>
        </div>
      </div>
      <NuxtLink to="/" class="lead__button">Back</NuxtLink>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      lead: {
        type: Object,
        default: null,
      },
      image: {
        type: Object,
        default: null,
      },
    }
  },
  async fetch() {
    this.lead = await fetch(
      `https://jsonplaceholder.typicode.com/users/${this.$route.params.id}`
    ).then((response) => response.json())
    this.image = await fetch(
      'https://randomuser.me/api/?results=1'
    ).then((response) => response.json())
  },
}
</script>

<style lang="scss" scoped>
.lead {
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  border-radius: 4px;
  width: 80vw;
  margin: 0 auto;
  margin-top: 32px;
  &__fetched {
    padding-bottom: 32px;
  }
}
.data {
  background-color: #fcfcfc;
  &__header {
    background-color: #fff;
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    justify-content: center;
    padding: 32px 48px;
    border-bottom: 1px solid darken($color: $border-color, $amount: 5);
  }
  &__name {
    margin-left: 16px;
  }
  &__body {
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
}
.data__summary,
.data__relation {
  padding: 16px 0;
  background-color: #ffffff;
  border-bottom: 1px solid darken($color: $border-color, $amount: 5);
}
.data__summary {
  background-color: #fcfcfc;
  display: flex;
  justify-content: space-between;
  padding: 32px 48px;
}
.data__relation {
  margin: 32px 18px;
  padding: 24px 32px;
  border-radius: 8px;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  border-bottom: 1px solid darken($color: $border-color, $amount: 5);
  &:not(:nth-child(2)) {
    margin-top: 0;
  }
}
.data__chunk {
  display: flex;
  flex-wrap: wrap;
  justify-content: start;
  gap: 16px;
  margin-top: 8px;
}
.chunk__group {
  p {
    &:nth-child(2) {
      color: #9994b8;
      font-size: 14px;
    }
  }
}
img {
  border-radius: 100%;
  border: 3px solid #fff;
  padding: 2px;
  transition: border 0.4s ease;
  border: 3px solid $green;
}
.lead__button {
  margin-left: 18px;
  margin-bottom: 32px;
  padding: 8px 32px;
  border-radius: 8px;
  border: 1px solid $primary;
  background: none;
  font-weight: bold;
  text-decoration: none;
  color: $default;
  cursor: pointer;
  outline: none;
  transition: all 0.4s ease;
  &:hover {
    background-color: $default;
    color: #fff;
    border: 1px solid #fff;
  }
}
</style>
