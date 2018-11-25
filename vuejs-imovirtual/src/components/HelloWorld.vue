<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <div v-for="value in values" :key="value.date" >
      <span>{{ value.value }}</span>
    </div>

    <Graph :data={values}></Graph>
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
      loading: true
    }
  },
  mounted () {
    axios
      .get('http://localhost:8081/?startDate=1543148511&endDate=1543234911')
      .then(response => {
        this.values = response.data
        console.log(this.values)
      })
      .catch(error => {
        console.log(error)
        this.errored = true
      })
      .finally(() => { this.loading = false })
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
