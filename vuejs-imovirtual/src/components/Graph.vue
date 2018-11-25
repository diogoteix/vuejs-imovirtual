<script>
import { Line } from 'vue-chartjs'

export default {
  extends: Line,
  props: ['data'],
  mounted () {
    // Overwriting base render method with actual data.
    console.log(this.data.values)
    this.renderChart({
      labels: this.data.values.map(a => new Date(a.date)),
      datasets: [
        {
          label: 'GitHub Commits',
          backgroundColor: '#f87979',
          data: this.data.values.map(a => a.value)
        }
      ]
    })
  }
}
</script>
