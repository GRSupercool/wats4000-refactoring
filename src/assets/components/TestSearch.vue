<!--TODO: Delete this file. It was experimental -->
<template>
  <div>
    <h2>Test Search</h2>

    <ul class="cities" v-if="results && results.list.length > 0">
        <li v-for="city in results.list">
            <h2>{{ city.name }}, {{ city.sys.country }}</h2>
            <p><router-link v-bind:to="{ name: 'CurrentWeather', params: { cityId: city.id } }">View Current Weather</router-link></p>
            <p v-for="weatherSummary in city.weather">
                <img v-bind:src="'http://openweathermap.org/img/w/' + weatherSummary.icon + '.png'" v-bind:alt="weatherSummary.main">
                <br>
                <b>{{ weatherSummary.main }}</b>
                <br>
                {{ weatherSummary.description }}
            </p>
            <dl class="current-weather">
                <dt>Current Temp</dt>
                <dd>{{ city.main.temp }}&deg;F</dd>
                <dt>Humidity</dt>
                <dd>{{ city.main.humidity }}%</dd>
                <dt>High</dt>
                <dd>{{ city.main.temp_max }}&deg;F</dd>
                <dt>Low</dt>
                <dd>{{ city.main.temp_min }}&deg;F</dd>
            </dl>
        </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'CitySearch',
  data () {
    return {
      results: null,
      errors: [],
      query: ''
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
  width: 15%;
  min-height: 300px;
  border: solid 1px #e8e8e8;
  padding: 10px;
  margin: 5px;
}

a {
  color: #42b983;
}
</style>


