<template>
  <div class="home">
    <div class="cards">
      <a class="card" v-for="beer in beers">
        <div v-bind:title="beer.tagline">
          <div class="card-hero" >
            <img v-bind:src="beer.image_url" width="288"/>
          </div>
          <div class="card-header">
            <h3>{{ beer.name }}</h3>
          </div>
          <div class="card-body">
            <p>{{ beer.description }}</p>
          </div>
        </div>
        <router-link :to="{name: 'About', params: {id: beer.id}}">More</router-link>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      beers: [],
      filter:{
        maxYear: false
      }
    }
  },
  created() {
    fetch('https://api.punkapi.com/v2/beers')
        .then(response => response.json())
        .then(json => {
          this.beers = json
        });
  }
}
</script>
