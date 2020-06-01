<template>
  <fusioncharts
    :type="type"
    :width="width"
    :height="height"
    :data-format="dataFormat"
    :data-source="dataSource"
  />
</template>

<script>
export default {
  props: {
    data: {
      type: Object,
      required: true
    }
  }
}
</script>
