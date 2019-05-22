<template>
  <div>
    <h2>
      Current Weather
      <span
        v-if="weatherData"
      >for {{ weatherData.name }}, {{weatherData.sys.country }}</span>
    </h2>
    <p>
      <router-link to="/">Home</router-link>|
      <router-link
        v-bind:to="{ name: 'Forecast', params: { cityId: $route.params.cityId } }"
      >View 5-Day Forecast</router-link>
    </p>
    <div v-if="weatherData && errors.length===0">
      <!-- TODO: Make weather summary be in a child component. -->
      <weather-summary v-bind:weatherData="weatherData.weather"></weather-summary>

     <!-- <div
        v-for="(weatherSummary,index) in weatherData.weather"
        :key="index"
        class="weatherSummary"
      >
        <img
          v-bind:src="'http://openweathermap.org/img/w/' + weatherSummary.icon + '.png'"
          v-bind:alt="weatherSummary.main"
        >
        <br>
        <b>{{ weatherSummary.main }}</b>
      </div> -->
      <!-- TODO: Make dl of weather data be in a child component. -->
      <dl>
        <dt>Current Temp</dt>
        <dd>{{ weatherData.main.temp }}&deg;F</dd>
        <dt>Humidity</dt>
        <dd>{{ weatherData.main.humidity }}%</dd>
        <dt>High</dt>
        <dd>{{ weatherData.main.temp_max }}&deg;F</dd>
        <dt>Low</dt>
        <dd>{{ weatherData.main.temp_min }}&deg;F</dd>
      </dl>
    </div>
    <div v-else-if="errors.length > 0">
      <h2>There was an error fetching weather data.</h2>
      <ul class="errors">
        <li v-for="(error,index) in errors" :key="index">{{ error }}</li>
      </ul>
    </div>
    <div v-else>
      <h2>Loading...</h2>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import {API} from '@/common/api';

export default {
  name: "CurrentWeather",
  data() {
    return {
      weatherData: null,
      errors: [],
      query: ""
    };
  },
  created() {
    // TODO: Improve base config for API
    API.get('find', {
      params: {
        q: this.query  
    }
  })
  created() {
   //axios.get("//api.openweathermap.org/data/2.5/weather", {
     // params: {
      //id: this.$route.params.cityId,
      //  units: "imperial",
      // APPID: "b3ee7227bdc31ea6aa6496c5b6f3b0c7"
     //  }
     // })
     
      // TODO: Improve base config for API
 API.get('weather', {
        params: {
        id: this.$route.params.cityId,
        }
      })

      .then(response => {
        this.weatherData = response.data;
      })
      .catch(error => {
        this.errors.push(error);
      });
  }
};

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.errors li {
  color: red;
  border: solid red 1px;
  padding: 5px;
}
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  width: 300px;
  min-height: 300px;
  border: solid 1px #e8e8e8;
  padding: 10px;
}
.weatherSummary {
  display: inline-block;
  width: 100px;
}
dl {
  padding: 5px;
  background: #e8e8e8;
}
dt {
  float: left;
  clear: left;
  width: 120px;
  text-align: right;
  font-weight: bold;
  color: blue;
}
dd {
  margin: 0 0 0 130px;
  padding: 0 0 0.5em 0;
}
dt::after {
  content: ":";
}
a {
  color: #42b983;
}
</style>

