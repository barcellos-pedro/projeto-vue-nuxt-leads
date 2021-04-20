<template>
  <main class="leads">
    <div class="leads__search">
      <input
        v-model="searchString"
        type="text"
        class="search__input"
        placeholder="Search by name or bs"
      />
    </div>
    <p v-if="$fetchState.pending">Fetching leads...</p>
    <p v-else-if="$fetchState.error">An error occurred :(</p>
    <div v-else>
      <NuxtLink to="/" class="leads_card">
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
.leads_card {
  margin: 1rem 0;
  max-width: 100%;
  text-decoration: none;
  color: $default;
}
</style>
