<template>
  <div class="container px-2 pb-4 mx-auto">
    <h1 class="text-xl font-bold">
      Casos de Covid em Poços de Caldas - MG
    </h1>
    <div class="py-4">
      <apexchart type="line" height="350" :options="totalCases" :series="series" />
    </div>
    <div class="py-4">
      <apexchart type="line" height="350" :options="confirmedOptions" :series="confirmed" />
    </div>

    <h2 class="mb-4 text-sm">
      Fonte: <a class="underline" href="https://pocosdecaldas.mg.gov.br/noticias/64500boletinsdiarios/">Prefeitura de Poços de Caldas</a>
    </h2>

    <Boxes />
  </div>
</template>

<script>
import CovidJson from '@/content/codiv_v3.json'

export default {
  name: 'Parse',
  data () {
    return {
      chartOptions: {
        chart: {
          locales: [{
            name: 'pt-br',
            options: {
              months: [
                'Janeiro',
                'Fevereiro',
                'Março',
                'Abril',
                'Maio',
                'Junho',
                'Julho',
                'Agosto',
                'Setembro',
                'Outubro',
                'Novembro',
                'Dezembro'
              ],
              shortMonths: [
                'Jan',
                'Fev',
                'Mar',
                'Abr',
                'Mai',
                'Jun',
                'Jul',
                'Ago',
                'Set',
                'Out',
                'Nov',
                'Dez'
              ],
              days: [
                'Domingo',
                'Segunda',
                'Terça',
                'Quarta',
                'Quinta',
                'Sexta',
                'Sábado'
              ],
              shortDays: ['Dom', 'Seg', 'Ter', 'Qua', 'Qui', 'Sex', 'Sab'],
              toolbar: {
                exportToSVG: 'Baixar SVG',
                exportToPNG: 'Baixar PNG',
                exportToCSV: 'Baixar CSV',
                menu: 'Menu',
                selection: 'Selecionar',
                selectionZoom: 'Selecionar Zoom',
                zoomIn: 'Aumentar',
                zoomOut: 'Diminuir',
                pan: 'Navegação',
                reset: 'Reiniciar Zoom'
              }
            }
          }
          ],
          defaultLocale: 'pt-br',
          type: 'line',
          stacked: false,
          height: 350,
          zoom: {
            type: 'x',
            enabled: true,
            autoScaleYaxis: true
          },
          toolbar: {
            autoSelected: 'zoom'
          }
        },
        markers: {
          size: 0
        },
        title: {
          text: 'Confirmados',
          align: 'left'
        },
        yaxis: {
          title: {
            text: 'casos'
          }
        },
        xaxis: {
          type: 'datetime'
        },
        tooltip: {
          shared: true
        }
      },
      series: [],
      confirmed: [],
      json: CovidJson
    }
  },
  computed: {
    confirmedOptions () {
      return {
        ...this.chartOptions,
        title: {
          text: 'Confirmados',
          align: 'left'
        },
        yaxis: {
          title: {
            text: 'casos'
          }
        }
      }
    },
    totalCases () {
      return {
        ...this.chartOptions,
        title: {
          text: 'Totais',
          align: 'left'
        },
        yaxis: {
          title: {
            text: 'casos'
          }
        }
      }
    }
  },
  mounted () {
    this.parseData()
  },
  methods: {
    parseData () {
      const confirmedList = []
      const cured = []
      const deaths = []

      const confirmedInterned = []
      const confirmedUti = []
      const confirmedCured = []
      const confirmedIsolated = []
      const confirmedDeath = []
      const investigationIsolated = []
      const investigationInterned = []
      const investigationUti = []
      const investigationDeath = []

      const nonResidentDeath = []

      this.json.cases.map((item) => {
        const date = this.formatDate(item.date)
        confirmedList.push({ x: date, y: this.calculateTotalobject(item.confirmed) })
        confirmedInterned.push({ x: date, y: item.confirmed.interned })
        confirmedUti.push({ x: date, y: item.confirmed.uti })
        confirmedCured.push({ x: date, y: item.confirmed.cured })
        confirmedIsolated.push({ x: date, y: item.confirmed.isolated })
        confirmedDeath.push({ x: date, y: item.confirmed.death })
        nonResidentDeath.push({ x: date, y: item.non_resident_death || 0 })
        investigationIsolated.push({ x: date, y: item.under_investigation.isolated })
        investigationInterned.push({ x: date, y: item.under_investigation.interned })
        investigationUti.push({ x: date, y: item.under_investigation.uti })
        investigationDeath.push({ x: date, y: item.under_investigation.death })

        cured.push({
          x: date,
          y: item.confirmed?.cured
        })

        deaths.push({
          x: date,
          y: item.confirmed?.death + (item.non_resident_death || 0)
        })
      })

      this.series = [
        { data: confirmedList, name: 'Confirmados' },
        { data: cured, name: 'Recuperados' },
        { data: deaths, name: 'Óbitos' }
      ]

      this.confirmed = [
        { data: confirmedInterned, name: 'Internados em Ala' },
        { data: confirmedUti, name: 'UTI' },
        { data: confirmedCured, name: 'Recuperados' },
        { data: confirmedIsolated, name: 'Isolados' },
        { data: confirmedDeath, name: 'Óbitos' },
        { data: nonResidentDeath, name: 'Óbitos de não-residentes' }
      ]
    },
    formatDate (date) {
      const year = date.substr(6, 4)
      const month = date.substr(3, 2)
      const day = date.substr(0, 2)
      const formatedDate = `${month}-${day}-${year} GMT`
      return formatedDate
    },
    calculateTotalobject (object) {
      let total = 0
      for (const key in object) {
        const element = object[key]
        total = total + element
      }
      return total
    }
  },
  head () {
    return {
      script: [{ src: 'https://identity.netlify.com/v1/netlify-identity-widget.js' }]
    }
  }
}
</script>
