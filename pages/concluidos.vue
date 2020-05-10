<template>
  <div class="container px-2 pb-4 mx-auto">
    <h1 class="text-xl font-bold">
      Casos de Covid em Poços de Caldas - MG
    </h1>

    <h2 class="text-lg font-bold">
      Investigação Concluída
    </h2>

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
          label: 'Descartado por exame laboratorial',
          borderColor: '#e99c2a',
          backgroundColor: 'transparent',
          data: covidData.map((item) => {
            const {
              tested_discarded: testedDiscarded
            } = item.investigation_finished

            return testedDiscarded
          })
        },
        {
          label: 'Alta por critério clínico',
          borderColor: '#df1d5f',
          backgroundColor: 'transparent',
          data: covidData.map((item) => {
            const {
              examined_discarded: examinedDiscarded
            } = item.investigation_finished

            return examinedDiscarded
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
      title: 'Investigação Concluída',
      meta: [
        { hid: 'description', name: 'description', content: 'Casos de Covid-19 em Poços de Caldas - MG' }
      ]
    }
  }
}
</script>
