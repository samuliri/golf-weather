<template>
  <div>
    <div class="search-box">
      <input 
        type="text" 
        class="search-bar" 
        placeholder="Gumböle"
        v-model="query"
        @keypress="fetchWeather"
      />
    </div>

    <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
      <div class="location-box">
        <div class="location">{{ weather.name }},  {{ weather.sys.country }}</div>
      </div>

      <div class="weather-box">
        <div class="temp">{{ Math.round(weather.main.temp)}}°C</div>
        <div class="weather">{{ weather.weather[0].main }}</div>
        <div class="wind">Wind {{ weather.wind.speed }} m/s</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Weather',
  data () {
    return {
      api_key: '978f0aac021459bcead1b7b57eda0502',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: 'Gumböle',
      weather: {}
    }
  },
  methods: {
    fetchWeather (e) {
      if (e.key == "Enter" || e == 'init') {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then(res => { return res.json(); })
          .catch(err => { console.log(err); })
          .then(this.setResults);
      }
    },
    setResults (results) {
      this.weather = results;
      console.log(this.weather);
    }
  },
  beforeMount(){
    this.fetchWeather('init')
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.search-box {
  margin: 0 auto 4rem;
  max-width: 300px;
}

.search-box, .search-bar {
  display: block;
  width: 100%;
  padding: 10px;

  color: #313131;
  font-size: 20px;

  appearance: none;
  border: none;
  outline: none;
  background: none;

  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.2);
  border-radius: 3px 16px 3px 16px;
  transition: 0.4s;
}

.search-box, .search-bar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.7);
  border-radius: 16px 3px 16px 3px;
}

.location-box {
  margin-bottom: 2rem;
}

.location-box .location {
  color: white;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.location-box .date {
  color: white;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}

.weather-box {
  text-align: center;
}

.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: white;
  font-size: 102px;
  font-weight: 900;

  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin-bottom: 1rem;

  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.weather-box .weather {
  color: white;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;

  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.weather-box .wind {
  color: white;
  font-size: 20px;
  font-weight: 500;
  font-style: italic;
}
</style>
