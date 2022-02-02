<template>
  <div class="about">
      <div v-bind:title="beers[$route.params.id - 1].tagline">
          <img v-bind:src="beers[$route.params.id - 1].image_url" width="288"/>
          <h3>{{ beers[$route.params.id - 1].name }}</h3>
          <p>{{ beers[$route.params.id - 1].description }}</p>
          <ul>
            <li><b>Ph level:</b><br> {{ beers[$route.params.id - 1].ph }}</li>
            <li><b>Food Pairing:</b><br></li>
            <ul>
              <li v-for="food in beers[$route.params.id - 1].food_pairing">
                {{ food }}
              </li>
            </ul>
            <li><b>Brewer tips:</b><br>{{ beers[$route.params.id - 1].brewers_tips }}</li>
            <li><b>Fermentation temp:</b><br>{{ beers[$route.params.id - 1].method.fermentation.temp.value }} {{ beers[$route.params.id - 1].method.fermentation.temp.unit }}</li>
            <li><b>Mash temp:</b><br></li>
            <ul>
              <li v-for="mash_temp in beers[$route.params.id - 1].method.mash_temp">
                <i>Temp:</i>
                {{mash_temp.temp.value}} {{mash_temp.temp.unit}}
                <i>Duration:</i>
                {{mash_temp.duration}}
              </li>
            </ul>
          </ul>
      </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      beers: []
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
