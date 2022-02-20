<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    Beer info here
  </div>
</template>

<script>
export default {
  name: 'MainPage',
  props: {
    msg: String
  },
  data() {
    return {
      loading: false,
      post: null,
      error: null,
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    fetchData() {
      this.error = this.pageData = null
      this.loading = true

      fetch('https://api.openbrewerydb.org/breweries?by_city=providence')
      .then(res => res.json())
      .then(data => {
        this.loading = false
        this.pageData = data
        console.log(this.pageData)
      })
      .catch(err => {
        this.error = String(err)
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
