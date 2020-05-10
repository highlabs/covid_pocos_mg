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
  props: {
    list: {
      type: Array,
      required: true
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
