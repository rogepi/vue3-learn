<template>
  <MyMarker></MyMarker>
</template>

<script>
import { provide, reactive, ref, readonly } from 'vue'
import MyMarker from './MyMarker.vue'

export default {
  components: {
    MyMarker,
  },
  setup() {
    // 添加响应性
    const location = ref('North Pole')
    const geolocation = reactive({
      longitude: 90,
      latitude: 135,
    })

    const updateLocation = () => {
      location.value = 'South Pole'
    }
    // 如果要确保通过 provide 传递的数据不会被 inject 的组件更改，
    // 我们建议对提供者的 property 使用 readonly。
    provide('location', readonly(location))
    provide('geolocation', geolocation)
    provide('updateLocation', updateLocation)
  },
  // 修改响应式 property
  // 当使用响应式 provide / inject 值时，尽可能在提供者内保持响应式 property 的任何更改。
  methods: {
    updateLocation() {
      this.location = 'South Pole'
    },
  },
}
</script>

<style>
</style>