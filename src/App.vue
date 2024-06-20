<template>
  <div id="app">
    <header>
      <nav class="navbar">
        <ul class="nav-list">
          <li><a href="https://ekarahmanaputri-project-cv.vercel.app/">Tugas 1</a></li>
          <li><a href="https://ekarahmanatugas2.netlify.app/">Tugas 2</a></li>
          <li><a href="https://tugasprakpbk.netlify.app/">Tugas 3</a></li>
          <li><a href="https://ekarahmanaputritugas4.netlify.app/">Tugas 4</a></li>
          <li><a href="https://ekarahmanaputri-landingpage.netlify.app/">Tugas 5</a></li>
          <li><a href="https://ekarahmanaputritugas6.netlify.app/">Tugas 6</a></li>
        </ul>
      </nav>
      <h2 class="heading">Aplikasi pendeteksi cuaca</h2>
    </header>
    <div class="container">
      <div class="container1">
        <p>Masukkan Nama Kota:</p>
        <input type="text" v-model="city" placeholder="Masukkan nama Kota">
      </div>
      <div class="button">
        <button @click="getWeather">Cek Cuaca</button>
      </div>
      <div id="result">
        <div v-if="weatherData">
          <h2 style="font-family: 'Alkatra', serif;">Cuaca di Kota {{ weatherData.name }}</h2>
          <h4>Temperature: {{ Math.round(weatherData.main.temp - 273.15) }}° C</h4>
          <h4>Feels like: {{ Math.round(weatherData.main.feels_like - 273.15) }}° C</h4>
          <h4>Humidity: {{ weatherData.main.humidity }} %</h4>
          <h4>Pressure: {{ weatherData.main.pressure }} hPa</h4>
          <h4>Wind speed: {{ weatherData.wind.speed }} m/s</h4>
          <h4>Wind direction: {{ weatherData.wind.deg }} degrees</h4>
        </div>
        <div v-else-if="error">
          <p>{{ error }}</p>
        </div>
      </div>
    </div>
    <footer class="footer">
      <span>&#169 Eka Rahmana Putri</span>
    </footer>
  </div>
</template>

<script>
export default {
  data() {
    return {
      city: '',
      weatherData: null,
      error: null,
    };
  },
  methods: {
    getWeather() {
      const url = `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=6de954dc6828fcd8e7e47721bdba6a7b`;
      fetch(url)
        .then(response => response.json())
        .then(data => {
          if (data.cod === '404') {
            this.error = 'Kota tidak di temukan. Silahkan masukkan lagi.';
            this.weatherData = null;
          } else {
            this.weatherData = data;
            this.error = null;
          }
        })
        .catch(error => {
          console.error('Error:', error);
          this.error = 'An error occurred. Please try again.';
          this.weatherData = null;
        });
    }
  }
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  background-size: cover;
}

header {
  background: #2A3132;
  box-shadow: 0 4px 8px rgb(210, 180, 180);
  color: #fff;
  padding: 10px;
  text-align: center;
  font-family: 'Alkatra', serif;
  text-shadow: 2px 2px 4px #000000;
}

.navbar {
  display: flex;
  justify-content: center;
  background: #336B87;
  padding: 10px 10px;
  
}

.nav-list {
  list-style: none;
  display: flex;
  gap: 15px;
}

.nav-list a {
  color: #fff;
  text-decoration: none;
  font-family: 'Domine', serif;
  font-size: 18px;
  padding: 5px 10px;
  border-radius: 5px;
  transition: background-color 0.3s;
}

.nav-list a:hover {
  background-color:#90AFC5;
}

.heading {
  margin: 10px 0;
  font-size: 36px;
}

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  background:#763636;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  width: 90%;
  max-width: 400px;
  border-radius: 8px;
  padding: 20px;
  margin: 20px auto;
}

.container1 {
  margin-bottom: 20px;
}

p {
  margin: 0;
  font-size: large;
  color: #fff;
  text-shadow: 2px 2px 4px #000;
  font-family: sans-serif;
}

input[type="text"] {
  margin-top: 10px;
  padding: 10px;
  font-size: 16px;
  border: none;
  border-radius: 4px;
  font-family: sans-serif;
  box-shadow: 0 2px 2px rgba(0, 0, 0, 0.1);
  background-color: black;
  color: #fff;
}

button {
  padding: 10px 20px;
  font-size: 16px;
  margin-top: 2%;
  font-family: sans-serif;
  background-color: #b85a65;
  color: #fff;
  text-shadow: 2px 2px 4px #000;
  border: none;
  border-radius: 3px;
  box-shadow: 0 2px 2px rgba(0, 0, 0, 0.1);
  cursor: pointer;
}

button:hover {
  background-color: #ca3537;
}

.container #result {
  margin-top: 2rem;
  color: #fff;
  font-family: 'Quicksand', sans-serif;
  text-shadow: 2px 2px 4px #000;
  font-size: large;
  line-height: 2rem;
  padding: 2rem;
}

.footer {
  font-size: large;
  font-family: 'Alkatra', serif;
  margin-top: 20px;
  text-align: center;
  color: #fff;
}
</style>
