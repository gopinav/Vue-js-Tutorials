<template>
  <div>
    <h1>{{ msg }}</h1>
    <div>
      <span v-for="(quote, i) in quotes" :key="i" v-html="quote.quote">
      </span>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'List of quotes',
      quotes: {},      
    }
  },
  created () {
    this.fetchData()
  },
  methods: {
    fetchData () {
      axios.get('https://quotes.rest/qod')
        .then(response => {
          console.log(response.data)
          this.quotes = response.data.contents.quotes
        })
        .catch(error => {
          console.log(error)
        })
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
