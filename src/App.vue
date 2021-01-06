<template>
  <div id="app">
    <main>
      <!-- Search box -->
      <div class="search-box">
        <input type="text" class="search-bar" />
      </div>
      <!-- Weather/Location box -->
      <div class="weather">
        <div class="location-box">
          <div class="location">Dtown, NJ</div>
          <div class="date">Tuesday January 5th, 2021</div>
        </div>
        <div class="weather-box">
          <div class="temperature">10F</div>
          <div class="weather-status">Cloudy</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: 'App'
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

.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  color: #313131;
  font-size: 20px;
  border: none;
  outline: none;
  background: none;
  box-shadow: 8px rgba(0, 0, 0, 0, 25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 16px;
  transition: 0.4s;
}

.search-box .search-bar:focus {
  box-shadow: 16px rgba(0, 0, 0, 0, 25);
  background-color: rgba(255, 255, 255, 0.75);
}
</style>
