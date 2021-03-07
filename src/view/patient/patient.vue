<template>
  <div class="monitor-page">
    <!-- 患者列表页面 -->
    <Screen></Screen>
  </div>
</template>

<script>
import Screen from '_c/screen'
import CountTo from '_c/count-to'
export default {
  name: 'patient_page',
  components: {
    CountTo,
    Screen
  },
  data () {
    return {
    }
  },
  methods: {
  }
}
</script>
<style lang="less">
  .size {
    width: 100%;
    height: 100%;
  }
</style>
