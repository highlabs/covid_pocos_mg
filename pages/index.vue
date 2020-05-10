<template>
  <div class="container px-2 pb-4 mx-auto">
    <h1 class="text-xl font-bold">
      Casos de Covid em Poços de Caldas - MG
    </h1>

    <LineChart :data="formatedData" />

    <h2 class="mb-4 text-lg font-bold">
      Descrição dos dados
    </h2>

    <Boxes />
  </div>
</template>

<script>
import LineChart from '@/components/Linechart'
import Boxes from '@/components/Boxes'
import CovidJson from '@/content/codiv_v3.json'

export default {
  components: {
    LineChart,
    Boxes
  },
  data () {
    return {
      datacollection: null,
      covidData: CovidJson
    }
  },
  computed: {
    formatedData () {
      const covidData = this.covidData
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
  },
  head () {
    return {
      title: 'Home',
      meta: [
        { hid: 'description', name: 'description', content: 'Casos de Covid-19 em Poços de Caldas - MG' }
      ]
    }
  }
}
</script>
