<template>
  <div class="container px-2 mx-auto">
    <h1 class="text-lg font-bold">
      Casos de Covid em Poços de Caldas - MG
    </h1>

    <div class="w-full my-8">
      <line-chart :width="null" :height="null" :chart-data="formatedData" />
    </div>
  </div>
</template>

<script>
import LineChart from '@/charts/LineChart.js'
import CovidJson from '@/content/codiv_v3.json'

export default {
  components: {
    LineChart
  },
  data () {
    return {
      datacollection: null
    }
  },
  computed: {
    formatedData () {
      const covidData = CovidJson

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
