<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <button v-on:click="displayVisited">Show Visited</button>
    <div v-if="unvisited" class="brewery-container">
      <div v-for="brewery in unvisited" v-bind:key="brewery.id">
        <div class="brewery-card">
        <h3>{{brewery.name}}</h3>
        <p>{{brewery.street}}, {{brewery.city}} {{brewery.state}}</p>
        <p>Brewery Type: {{brewery.brewery_type}}</p>
        <a v-bind:href="brewery.website_url" target="_blank">Learn more</a>
        <button @click="addVisited(brewery.id)">Mark as Visited</button>
        </div>
      </div>
    </div>
    <div v-if="showVisited" class="brewery-container">
      <div v-for="brewery in visited" v-bind:key="brewery.id">
        <div class="brewery-card visited">
        <h3>{{brewery.name}}</h3>
        <p>{{brewery.street}}, {{brewery.city}} {{brewery.state}}</p>
        <p>Brewery Type: {{brewery.brewery_type}}</p>
        <a v-bind:href="brewery.website_url" target="_blank">Learn more</a>
        <!-- <button @click="addVisited(brewery.id)">Mark as Visited</button> -->
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
      visited: [],
      unvisited: [],
      showVisited: false
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
        this.unvisited = [...data]
        console.log(this.unvisited)
      })
      .catch(err => {
        this.error = String(err)
      })
    },
    addVisited(id) {
      let selectedIndex = this.unvisited.findIndex(el => el.id === id)
      let selectedBrewery = this.unvisited.splice(selectedIndex, 1)
      this.visited = [...this.visited, ...selectedBrewery]
    },
    displayVisited() {
      this.showVisited = true
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
}
.brewery-card {
border: 2px solid black;
width: 400px;
display: flex;
flex-direction: column;
justify-content: space-evenly;
align-items: center;
margin: 20px;
}

button {
  padding: 5px 20px;
  margin: 10px;
}

.visited {
  background-color: lightgreen;
}
</style>
