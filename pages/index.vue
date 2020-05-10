<template>
  <div class="container px-2 pb-4 mx-auto">
    <h1 class="text-xl font-bold">
      Casos de Covid em Poços de Caldas - MG
    </h1>

    <LineChart :data="covidData" />

    <h2 class="mb-4 text-lg font-bold">
      Descrição dos dados
    </h2>

    <div class="flex flex-wrap items-stretch">
      <div v-for="box in boxList" :key="box.title" class="flex items-stretch w-full md:w-1/3">
        <div class="w-full p-4 m-1 border-4" :class="box.color">
          <h3 class="font-bold">
            {{ box.title }}
          </h3>
          <p>{{ box.description }}</p>
          <ul>
            <li v-for="item in box.list" :key="item">
              {{ item }}
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import LineChart from '@/components/Linechart'
import CovidJson from '@/content/codiv_v3.json'

export default {
  components: {
    LineChart
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

<style scoped>
.yellow-border {
  border-color: #e99c2a
}
.blue-border {
  border-color: #6898c7
}
.pink-border {
  border-color: #df1d5f;
}
.green-boder {
  border-color: #358b91;
}
ul {
  @apply pl-8
}
li {
  @apply list-disc
}
</style>
