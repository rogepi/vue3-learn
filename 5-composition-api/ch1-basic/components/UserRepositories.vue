<template></template>

<script>
// src/components/UserRepositories.vue
import useUserRepositories from '../composables/useUserRepositories'
import useRepositoryNameSearch from '../composables/useRepositoryNameSearch'
import { toRefs } from 'vue'

export default {
  components: {
    RepositoriesFilters,
    RepositoriesSortBy,
    RepositoriesLists,
    props: {
      user: {
        type: String,
        required: true,
      },
    },
    setup(props) {
      const { user } = toRefs(props)

      const { repositories, getUserRepositories } = useUserRepositories(user)

      const {
        searchQuery,
        repositoriesMatchingSearchQuery,
      } = useRepositoryNameSearch(repositories)

      return {
        repositories: repositoriesMatchingSearchQuery,
        getUserRepositories,
        searchQuery,
      }
    },
    data() {
      return {
        filters: {},
      }
    },
    computed: {
      filteredRepositories() {},
    },
    methods: {
      updateFilters() {},
    },
  },
}
</script>

<style>
</style>