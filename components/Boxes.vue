<template>
  <div class="flex flex-wrap items-stretch">
    <div v-for="box in list" :key="box.title" class="flex items-stretch w-full md:w-1/3">
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
</template>

<script>
export default {
  name: 'Boxes',
  data () {
    return {
      list: [
        {
          title: 'Suspeitos notificados',
          description: 'Esses dados agrupam todos os números notificados em poços.',
          color: 'blue-border'
        },
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
  }
}
</script>

<style scoped>
ul {
  @apply pl-8
}
li {
  @apply list-disc
}
.yellow-border {
  border-color: #e99c2a
}
.blue-border {
  border-color: #6898c7
}
.pink-border {
  border-color: #df1d5f;
}
.green-border {
  border-color: #358b91;
}
</style>
