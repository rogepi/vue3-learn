<template>
  <div>
    <span>{{ count }}</span>
    <button @click="count++">Increment count</button>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    const count = ref(0);
    return {
      // 当 ref 作为渲染上下文 (从 setup() 中返回的对象) 上的 property 返回并可以在模板中被访问时，
      // 它将自动展开为内部值。不需要在模板中追加 .value：
      count,
    };
  },
};

// 当 ref 作为响应式对象的 property 被访问或更改时，
// 为使其行为类似于普通 property，它会自动展开内部值：
const count = ref(0);
const state = reactive({
  count,
});

console.log(state.count); // 0

state.count = 1;
console.log(count.value); // 1

// 如果将新的 ref 赋值给现有 ref 的 property，将会替换旧的 ref：

const otherCount = ref(2);

state.count = otherCount;
console.log(state.count); // 2
console.log(count.value); // 1

// Ref 展开仅发生在被响应式 Object 嵌套的时候。
// 当从 Array 或原生集合类型如 Map访问 ref 时，不会进行展开：

const books = reactive([ref('Vue 3 Guide')])
// 这里需要 .value
console.log(books[0].value)

const map = reactive(new Map([['count', ref(0)]]))
// 这里需要 .value
console.log(map.get('count').value)
</script>

<style>
</style>