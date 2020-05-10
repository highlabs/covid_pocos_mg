<template>
  <div class="w-full my-8">
    <line-chart :width="null" :height="null" :chart-data="data" />
  </div>
</template>

<script>
import LineChart from '@/charts/LineChart.js'

export default {
  components: {
    LineChart
  },
  props: {
    data: {
      type: Array,
      required: true
    }
  }
}
</script>
