<template>
  <div class="container px-2 pb-4 mx-auto">
    <h1 class="text-xl font-bold">
      Casos de Covid em Poços de Caldas - MG
    </h1>

    <h2 class="text-lg font-bold">
      Casos Confirmados
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
          label: 'Internados em ala',
          borderColor: '#FDE74C',
          backgroundColor: 'transparent',
          data: covidData.map((item) => {
            const {
              interned
            } = item.confirmed

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
            } = item.confirmed

            return uti
          })
        },
        {
          label: 'Recuperados',
          borderColor: '#84DCCF',
          backgroundColor: 'transparent',
          data: covidData.map((item) => {
            const {
              cured
            } = item.confirmed

            return cured
          })
        },
        {
          label: 'Em isolamento domiciliar',
          borderColor: '#5BC0EB',
          backgroundColor: 'transparent',
          data: covidData.map((item) => {
            const {
              isolated
            } = item.confirmed

            return isolated
          })
        },
        {
          label: 'Óbitos confirmados',
          borderColor: '#C3423F',
          backgroundColor: 'transparent',
          data: covidData.map((item) => {
            const {
              death
            } = item.confirmed

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
      title: 'Casos Confirmados',
      meta: [
        { hid: 'description', name: 'description', content: 'Casos de Covid-19 em Poços de Caldas - MG' }
      ]
    }
  }
}
</script>
