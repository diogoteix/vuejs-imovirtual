<template>
  <div class="hello">
    <h2>Imovirtual</h2>
    <Graph :styles="myStyles" v-if="!loading && imovirtual.length > 0" v-bind:values="imovirtual"></Graph>

    <h2>Idealista</h2>
    <Graph :styles="myStyles" v-if="!loading && idealista.length > 0" v-bind:values="idealista"></Graph>

  </div>
</template>

<script>
import axios from 'axios'
import Graph from './Graph'

export default {
  name: 'HelloWorld',
  components: {
    Graph
  },
  data () {
    return {
      values: [],
      loading: true,
      idealista: [],
      imovirtual: []
    }
  },
  mounted () {
    axios
      .get('https://api-imovirtual.herokuapp.com/?startDate=1543148511&endDate=1543234911')
      .then(response => {
        this.values = response.data
        console.log(this.values)
        this.imovirtual = this.values.filter(obj => {
          return obj.source === 'imovirtual'
        })
        this.idealista = this.values.filter(obj => {
          return obj.source === 'idealista'
        })
      })
      .catch(error => {
        console.log(error)
        this.errored = true
      })
      .finally(() => { this.loading = false })
  },
  computed: {
    myStyles () {
      return {
        height: `400px`,
        position: 'relative'
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
