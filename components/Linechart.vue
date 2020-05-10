<template>
  <div class="w-full my-8">
    <line-chart :width="null" :height="null" :chart-data="formatedData" />
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
  },
  computed: {
    formatedData () {
      const covidData = this.data

      const formatedCovidData = [
        {
          label: 'Suspeitos Notificados',
          borderColor: '#6898c7',
          backgroundColor: 'transparent',
          data: covidData.map(item => item.total_notifications)
        },
        {
          label: 'Investigação Concluída',
          borderColor: '#e99c2a',
          backgroundColor: 'transparent',
          data: covidData.map((item) => {
            const {
              tested_discarded: testedDiscarded,
              examined_discarded: examinedDiscarded
            } = item.investigation_finished

            const total = testedDiscarded + examinedDiscarded

            return total
          })
        },
        {
          label: 'Casos suspeitos em investigação',
          borderColor: '#df1d5f',
          backgroundColor: 'transparent',
          data: covidData.map((item) => {
            const {
              isolated,
              interned,
              uti,
              death
            } = item.under_investigation
            const total = isolated + interned + uti + death

            return total
          })
        },
        {
          label: 'Casos confirmados',
          borderColor: '#358b91',
          backgroundColor: 'transparent',
          data: covidData.map((item) => {
            const {
              interned,
              uti,
              cured,
              isolated,
              death
            } = item.confirmed

            const total = interned + uti + cured + isolated + death

            return total
          })
        }
      ]

      const dateLabels = covidData.map(item => item.date)

      const dataSet = {
        labels: dateLabels,
        datasets: formatedCovidData
      }
      return dataSet
    }
  }
}
</script>
