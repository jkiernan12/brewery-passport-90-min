<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div v-if="pageData" class="brewery-container">
      {{pageData[0].name}}
      <div v-for="brewery in pageData" v-bind:key="brewery.id">
        {{brewery.name}}
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
}
</style>
