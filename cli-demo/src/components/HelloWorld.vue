<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div>
      <span v-for="(quote, i) in quotes" :key="i" v-html="quote.content">
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
      axios.get('http://quotesondesign.com/wp-json/posts?filter[orderby]=rand&filter[posts_per_page]=10')
        .then(response => {
          console.log(response.data)
          this.quotes = response.data
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
