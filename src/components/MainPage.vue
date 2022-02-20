<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div v-if="pageData" class="brewery-container">
      <div v-for="brewery in pageData" v-bind:key="brewery.id">
        <div class="brewery-card">
        <h3>{{brewery.name}}</h3>
        <p>{{brewery.street}}, {{brewery.city}} {{brewery.state}}</p>
        <p>Brewery Type: {{brewery.brewery_type}}</p>
        <a v-bind:href="brewery.website_url" target="_blank">Learn more</a>
        </div>
      </div>
    </div>
    <div v-if="loading">Loading</div>
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
.brewery-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
  align-items: stretch;
}
.brewery-card {
border: 2px solid black;
width: 400px;
height: 100%;
}
</style>
