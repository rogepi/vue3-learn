// MyBook.vue
<template>
  <!-- 从 setup 返回的 refs 在模板中访问时是被自动解开的，
  因此不应在模板中使用 .value -->

  <div>{{ readersNumber }} {{ book.title }}</div>
</template>

<script>
import { ref, reactive } from 'vue'
export default {
  setup() {
    const readersNumber = ref(0)
    const book = reactive({ title: 'Vue 3 Guide' })

    // expose to template
    return {
      readersNumber,
      book,
    }
  },
}
</script>