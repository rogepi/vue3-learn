<template></template>

<script>
// src/components/UserRepositories.vue

import { fetchUserRepositories } from '@/api/repositories'
import { ref, onMounted, watch, toRefs, computed } from 'vue'

export default {
  components: { RepositoriesFilters, RepositoriesSortBy, RepositoriesList },
  props: {
    user: {
      type: String,
      required: true,
    },
  },
  setup(props) {
    // 使用 `toRefs` 创建对prop的 `user` property 的响应式引用
    const { user } = toRefs(props)
    // 确保我们的侦听器能够对 user prop 所做的更改做出反应

    const repositories = ref([])
    const getUserRepositories = async () => {
      repositories.value = await fetchUserRepositories(user.value)
    }

    onMounted(getUserRepositories) // on `mounted` call `getUserRepositories`

    // 在用户 prop 的响应式引用上设置一个侦听器
    watch(user, getUserRepositories)

    const searchQuery = ref('')
    const repositoriesMatchingSearchQuery = computed(() => {
      return repositories.value.filter((repository) =>
        repository.name.includes(searchQuery.value)
      )
    })
    return {
      repositories,
      getUserRepositories,
      searchQuery,
      repositoriesMatchingSearchQuery,
    }
  },
  data() {
    return {
      filters: {}, // 3
      searchQuery: '', // 2
    }
  },
  computed: {
    filteredRepositories() {}, // 3
    repositoriesMatchingSearchQuery() {}, // 2
  },
  watch: {
    user: 'getUserRepositories', // 1
  },
  methods: {
    updateFilters() {}, // 3
  },
}
</script>

<style>
</style>