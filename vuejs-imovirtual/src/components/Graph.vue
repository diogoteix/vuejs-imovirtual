<script>
import { Line } from 'vue-chartjs'

export default {
  extends: Line,
  props: ['data'],
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
    console.log(this.data.values)
    this.renderChart({
      labels: this.data.values.map(a => this.getFormattedDate(new Date(a.date))),
      datasets: [
        {
          label: 'Preço Médio',
          borderColor: '#0099ff',
          backgroundColor: 'rgba(0, 153, 255, 0.2)',
          data: this.data.values.map(a => a.median)
        },
        {
          label: 'Preço Máximo',
          borderColor: '#ff0000',
          backgroundColor: 'rgba(255, 0, 0, 0.1)',
          data: this.data.values.map(a => a.max)
        },
        {
          label: 'Preço Mínimo',
          borderColor: '#33cc33',
          backgroundColor: 'rgba(51, 204, 51, 0.5)',
          data: this.data.values.map(a => a.min)
        }
      ]
    })
  }
}
</script>
