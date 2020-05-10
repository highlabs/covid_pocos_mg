<template>
  <div class="container px-2 pb-4 mx-auto">
    <h1 class="text-xl font-bold">
      Casos de Covid em Poços de Caldas - MG
    </h1>

    <h2 class="text-lg font-bold">
      Suspeitos Notificados
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
          label: 'Em isolamento domiciliar',
          borderColor: '#5BC0EB',
          backgroundColor: 'transparent',
          data: covidData.map((item) => {
            const {
              isolated
            } = item.under_investigation

            return isolated
          })
        },
        {
          label: 'Internados em ala',
          borderColor: '#FDE74C',
          backgroundColor: 'transparent',
          data: covidData.map((item) => {
            const {
              interned
            } = item.under_investigation

            return interned
          })
        },
        {
          label: 'Internados em UTI',
          borderColor: '#9BC53D',
          backgroundColor: 'transparent',
          data: covidData.map((item) => {
            const {
              uti
            } = item.under_investigation

            return uti
          })
        },
        {
          label: 'Óbitos em investigação',
          borderColor: '#C3423F',
          backgroundColor: 'transparent',
          data: covidData.map((item) => {
            const {
              death
            } = item.under_investigation

            return death
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
      title: 'Suspeitos Notificados',
      meta: [
        { hid: 'description', name: 'description', content: 'Casos de Covid-19 em Poços de Caldas - MG' }
      ]
    }
  }
}
</script>
