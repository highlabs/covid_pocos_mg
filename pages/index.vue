<template>
  <div class="container px-2 pb-4 mx-auto">
    <h1 class="text-xl font-bold">
      Casos de Covid em Poços de Caldas - MG
    </h1>

    <LineChart :data="covidData" />

    <h2 class="mb-4 text-lg font-bold">
      Descrição dos dados
    </h2>

    <Boxes :list="boxList" />
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
      covidData: CovidJson,
      boxList: [
        {
          title: 'Investigação concluída',
          description: 'Esses dados agrupam os seguintes números:',
          color: 'yellow-border',
          list: [
            'Descartado por exame laboratorial',
            'Alta por critério clínico'
          ]
        },
        {
          title: 'Casos suspeitos em investigação',
          desc: 'Esses dados agrupam os seguintes números:',
          color: 'pink-border',
          list: [
            'Em isolamento domiciliar (casos leves, sem indicação de realizar exame conforme Ministério da Saúde',
            'Internados em ala',
            'Internados em UTI',
            'Óbitos em investigação'
          ]
        },
        {
          title: 'Casos Confirmados',
          desc: 'Esses dados agrupam os seguintes números:',
          color: 'green-border',
          list: [
            'Internados em ala',
            'Internados em UTI',
            'Recuperados',
            'Em isolamento domiciliar',
            'Óbitos confirmados'
          ]
        }
      ]
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
