<template>
  <div id="app">
    <main>
      <!-- Search box -->
      <div class="search-box">
        <input
          type="text"
          class="search-bar"
          placeholder="Search for a city..."
          v-model="searchQuery"
          @keypress.enter="getWeather()"
        />
        <button class="search-btn" @click="getWeather()">
          <span class="search-btn-arrow">></span>
        </button>
      </div>
      <!-- Weather/Location box -->
      <div class="weather" v-if="typeof weather.main == 'undefined'">
        <div class="location-box">
          <div class="location">Location</div>
          <div class="date">{{ today }}</div>
        </div>
        <div class="weather-box">
          <div class="temperature">Temp</div>
          <div class="weather-status">Status</div>
        </div>
      </div>

      <div class="weather" v-else>
        <div class="location-box">
          <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
          <div class="date">{{ today }}</div>
        </div>
        <div class="weather-box">
          <div class="temperature">10°F</div>
          <div class="weather-status">Cloudy</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'App',
  data: () => ({
    apiKey: process.env.VUE_APP_API_KEY,
    urlBase: 'https://api.openweathermap.org/data/2.5/weather?q=',
    searchQuery: '',
    weather: {},
    today: ''
  }),
  methods: {
    async getWeather() {
      console.log('hey');
      try {
        const res = await axios.get(this.urlBase + this.searchQuery + '&appid=' + this.apiKey);
        this.weather = res.data;
        console.log(this.weather);
      } catch (e) {
        console.log(e);
      }
    },
    getOrdinalNumber(num) {
      let selector;
      if (num <= 0) {
        selector = 4;
      } else if ((num > 3 && num < 21) || num % 10 > 3) {
        selector = 0;
      } else {
        selector = num % 10;
      }
      return num + ['th', 'st', 'nd', 'rd', ''][selector];
    },
    getDate() {
      const d = new Date();
      const months = [
        'January',
        'February',
        'March',
        'April',
        'May',
        'June',
        'July',
        'August',
        'September',
        'October',
        'November',
        'December'
      ];
      const month = months[d.getMonth()];
      const dayWO = d.getDate();
      const day = this.getOrdinalNumber(dayWO);
      const year = d.getFullYear();

      this.today = month + ' ' + day + ', ' + year;
      console.log(this.today);
    }
  },
  created() {
    this.getDate();
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'montserrat', sans-serif;
}

#app {
  background-image: url('./assets/cold-bg.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}

main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
}

.search-box {
  width: 100%;
  margin-bottom: 30px;
}

.search-bar {
  display: inline-block;
  width: 95%;
  height: 60px;
  padding: 15px;
  color: #313131;
  font-size: 30px;
  font-style: italic;
  border: none;
  outline: none;
  background: none;
  box-shadow: 8px rgba(0, 0, 0, 0, 25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 16px 0 0 16px;
  transition: 0.4s;
}

.search-bar:focus {
  box-shadow: 16px rgba(0, 0, 0, 0, 25);
  background-color: rgba(255, 255, 255, 0.75);
}

.search-btn {
  display: inline-block;
  width: 5%;
  height: 60px;
  color: #313131;
  font-size: 30px;
  border: none;
  outline: none;
  background: none;
  box-shadow: 8px rgba(0, 0, 0, 0, 25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0 16px 16px 0;
}

.search-btn:hover {
  cursor: pointer;
}

.search-btn:active {
  color: rgba(255, 255, 255, 0.75);
}

.search-btn-arrow {
  font-weight: 800;
}

.location {
  color: white;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.date {
  color: white;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}

.weather-box {
  text-align: center;
}

.temperature {
  display: inline-block;
  padding: 10px 25px;
  color: white;
  font-size: 102px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.weather-status {
  color: white;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0, 25);
}
</style>
