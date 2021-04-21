<template>
  <main class="display">
    <div class="display__search">
      <input
        v-model="searchString"
        type="text"
        class="search__input"
        placeholder="Search by name or bs"
      />
    </div>
    <div v-if="$fetchState.pending" class="display__fetching">
      <loading-spinner />
    </div>
    <p v-else-if="$fetchState.error" class="display__error">
      An error occurred. Try again.
    </p>
    <div v-else>
      <div class="display__legend">
        <p></p>
        <p>Name</p>
        <p>E-mail</p>
        <p>Company</p>
        <p>Phone</p>
        <p>Company BS</p>
      </div>
      <NuxtLink to="/" class="display_card">
        <lead-card v-for="lead in searchLead" :key="lead.id" :lead="lead" />
      </NuxtLink>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      leads: [],
      searchString: undefined,
    }
  },
  async fetch() {
    this.leads = await fetch(
      'https://jsonplaceholder.typicode.com/users'
    ).then((response) => response.json())
  },
  fetchDelay: 1000,
  computed: {
    searchLead() {
      if (this.searchString === '' || this.searchString === undefined) {
        return this.leads
      }
      const byName = this.leads.filter((lead) =>
        lead.name.toLowerCase().includes(this.searchString.toLowerCase())
      )
      const byCompanyBs = this.leads.filter((lead) =>
        lead.company.bs.toLowerCase().includes(this.searchString.toLowerCase())
      )
      const result = [...byName, ...byCompanyBs]
      return Array.from(new Set(result))
    },
  },
}
</script>

<style lang="scss" scoped>
.display__search {
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
.display__legend {
  display: grid;
  grid-template-columns: 11% 16% 24% 16% 10% 22%;
  text-align: center;
  margin-top: 2rem;
  @media (max-width: 768px) {
    display: none;
  }
  p {
    color: #7d7d7d;
  }
}
.display_card {
  margin: 1rem 0;
  max-width: 100%;
  text-decoration: none;
  color: $default;
}
.display__fetching,
.display__error {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 20vh;
}
</style>
