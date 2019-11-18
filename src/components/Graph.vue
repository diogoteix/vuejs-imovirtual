<script>
import { Line } from 'vue-chartjs'

export default {
  extends: Line,
  props: ['values'],
  data () {
    return {
      options: {
        responsive: true,
        maintainAspectRatio: false,
        pan: {
          // Boolean to enable panning
          enabled: true,

          // Panning directions. Remove the appropriate direction to disable
          // Eg. 'y' would only allow panning in the y direction
          mode: 'xy'
        },
        // Container for zoom options
        zoom: {
          // Boolean to enable zooming
          enabled: true,

          // Zooming directions. Remove the appropriate direction to disable
          // Eg. 'y' would only allow zooming in the y direction
          mode: 'xy'
        }
      }
    }
  },
  methods: {
    getFormattedDate: function (date) {
      var dd = date.getDate()
      var mm = date.getMonth() + 1

      if (dd < 10) {
        dd = '0' + dd
      }
      if (mm < 10) {
        mm = '0' + mm
      }

      return dd + '/' + mm
    }
  },
  mounted () {
    // Overwriting base render method with actual data.
    console.log(this.values)
    this.renderChart(
      {
        labels: this.values.map(a => this.getFormattedDate(new Date(a.date))),
        datasets: [
          {
            label: 'Preço Médio',
            borderColor: '#0099ff',
            backgroundColor: 'rgba(0, 153, 255, 0.2)',
            data: this.values.map(a => a.median <= 5000 ? a.median : 5000)
          },
          {
            label: 'Preço Máximo',
            borderColor: '#ff0000',
            backgroundColor: 'rgba(255, 0, 0, 0.1)',
            data: this.values.map(a => a.max <= 5000 ? a.max : 5000)
          },
          {
            label: 'Preço Mínimo',
            borderColor: '#33cc33',
            backgroundColor: 'rgba(51, 204, 51, 0.5)',
            data: this.values.map(a => a.min)
          }
        ]
      },
      this.options
    )
  }
}
</script>
