<template>
  <div class="container p-0">
    <div class="d-flex">
      <div class="card main-div w-100">
        <div class="p-3">
          <h2 class="mb-1 day">{{ currentDay }}</h2>
          <p class="text-light date mb-0">{{ currentDate }}</p>
          <small>{{ currentTime }}</small>
          <h2 class="place">
            <i class="fas fa-map-marker-alt"></i> {{ city }}, {{ country }}
          </h2>
          <div class="temp">
            <h1 class="weather-temp">{{ Math.round(temperature) }}&deg;</h1>
            <h2 class="text-light">{{ description }}</h2>
          </div>
        </div>
      </div>
      <div class="card card-2 w-100">
        <table class="m-4">
          <tbody>
            <tr>
              <th>Windstärke</th>
              <td>{{ windSpeed }} km/h</td>
            </tr>
            <tr>
              <th>Feuchtigkeit</th>
              <td>{{ humidity }}%</td>
            </tr>
            <tr>
              <th>Regenwahrscheinlichkeit</th>
              <td>{{ rainProbability }}%</td>
            </tr>
          </tbody>
        </table>

        <daysWeather></daysWeather>
        <div id="div_Form" class="d-flex m-3 justify-content-center">
          <form @submit.prevent="changeCity">
            <input type="text" v-model="newCity" placeholder="Neuer Ort" class="form-control mr-2">
            <input type="submit" value="Ort ändern" class="btn change-btn btn-primary">
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import daysWeather from './daysWeather.vue';

export default {
  name: 'myWeather',
  components: {
    daysWeather,
  },
  data() {
    return {
      city: 'Magdeburg',
      country: 'Deutschland',
      newCity: '',
      temperature: null,
      description: null,
      windSpeed: null,
      humidity: null,
      rainProbability: null,
      weatherData: null,
      currentDate: '',
      currentTime: '',
      currentDay: '',
    };
  },
  methods: {
    async fetchWeather() {
      try {
        const response = await axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=7e9510c437c764a83a929511dc6ee3a3&units=metric&lang=de`);
        const weatherData = response.data;
        this.city = weatherData.name;
        this.country = weatherData.sys.country;
        this.temperature = weatherData.main.temp;
        this.description = weatherData.weather[0].description;
        this.windSpeed = weatherData.wind.speed;
        this.humidity = weatherData.main.humidity;
        this.rainProbability = weatherData.clouds.all; // Wolkenbedeckung als Regenwahrscheinlichkeit
        this.weatherData = weatherData;
        this.updateDateTime();
        console.log(this.temperature, this.description); // Debug-Ausgabe
      } catch (error) {
        console.error(error);
      }
    },
    changeCity() {
      this.city = this.newCity;
      this.fetchWeather();
    },
    updateDateTime() {
      const now = new Date();
      this.currentDate = now.toLocaleDateString('de-DE');
      this.currentTime = now.toLocaleTimeString('de-DE', {
        hour: '2-digit',
        minute: '2-digit',
      });
      this.currentDay = now.toLocaleDateString('de-DE', { weekday: 'long' });
    },
  },
  created() {
    this.fetchWeather();
  },
};
</script>

<style>
/* Globale Einstellungen für den Body */
body {
  background-color: #343d4b;
  /* Hintergrundfarbe */
  color: #ffffff;
  /* Textfarbe auf der gesamten Seite */
}

/* Stil für die Kopfzeile */
.header {
  background-color: #1e2532;
  /* Hintergrundfarbe der Kopfzeile */
  border-radius: 30px;
  /* Abgerundete Ecken */
}

/* Stil für den Such-Button */
.btn-search {
  background-image: linear-gradient(to right, rgb(0, 91, 210), rgb(224, 0, 224));
  /* Farbverlauf für den Button */
  color: #ffffff;
  /* Textfarbe für den Button */
}

/* Stil für die Anzeige der Wettertemperatur */
.weather-temp {
  margin: 0;
  font-weight: 700;
  font-size: 4em;
  /* Schriftgröße */
}

/* Stil für die Tagesanzeige */
h2.mb-1.day {
  font-size: 3rem;
  /* Schriftgröße */
  font-weight: 400;
}

/* Stil für die Hauptwetterkarte */
.main-div {
  border-radius: 30px;
  /* Abgerundete Ecken */
  background-image: url("https://www.capetownetc.com/wp-content/uploads/2022/09/pexels-jonathan-petersson-1237119-1024x681.jpg");
  /* Hintergrundbild */
  background-size: cover;
  /* Hintergrundbild skalieren */
  background-position: center;
  /* Hintergrundbild zentrieren */
  background-blend-mode: overlay;
  /* Mischmodus des Hintergrundbildes */
  background-color: rgba(0, 0, 0, 0.301);
  /* Hintergrundfarbe mit Transparenz */
  background-repeat: no-repeat;
  /* Hintergrundbild nicht wiederholen */
  min-height: 300px;
  /* Mindesthöhe für die Hauptkarte */
  position: relative;
  /* Positionierung des enthaltenen Elements .temp */
  color: #ffffff;
  /* Textfarbe für die Hauptkarte */
}

/* Stil für die Anzeige der Temperatur in der Hauptwetterkarte */
.temp {
  position: absolute;
  bottom: 10px;
  /* Abstand von unten */
  left: 10px;
  /* Abstand von links */
}

/* Vergrößern der Hauptwetterkarte beim Hover */
.main-div:hover {
  transform: scale(1.1);
  transition: transform 0.8s ease-in-out;
  /* Übergangseffekt */
  z-index: 1;
  /* Z-Index für Überlagerung */
}

/* Stil für die zweite Wetterkarte mit zusätzlichen Informationen */
.card-2 {
  background-color: #242b34;
  /* Hintergrundfarbe */
  border-radius: 30px;
  /* Abgerundete Ecken */
  color: #ffffff;
  /* Textfarbe */
  min-height: 200px;
  /* Mindesthöhe */
  margin-left: 1.5rem;
  /* Abstand nach links */
}

/* Stil für die Kartendetails */
.card-details {
  margin-left: 19px;
  /* Abstand nach links */
}

/* Stil für die h1-Elemente in der linken Ecke */
.h1_left {
  position: absolute;
  bottom: 25px;
  /* Abstand von unten */
  left: 16px;
  /* Abstand von links */
  font-size: 3vw;
  /* Schriftgröße in vw */
  line-height: 1.2;
  /* Zeilenhöhe */
}

/* Stil für die h3-Elemente in der linken Ecke */
.h3_left {
  position: absolute;
  left: 16px;
  /* Abstand von links */
  font-size: 2vw;
  /* Schriftgröße in vw */
  line-height: 0.5;
  /* Zeilenhöhe */
}

/* Stil für kleine Elemente innerhalb der h3-Elemente */
.h3_left small {
  font-size: 1rem;
  /* Schriftgröße */
}

/* Stil für die Tabelle */
table {
  border-collapse: separate;
  /* Zellen nicht zusammenziehen */
  border-spacing: 15px;
  /* Abstand zwischen Zellen */
  width: 85%;
  /* Breite der Tabelle */
  text-align: left;
  /* Textausrichtung */
  max-width: 600px;
  /* Maximale Breite */
  margin: 0 auto;
  /* Zentrierung */
  color: #ffffff;
  /* Textfarbe */
}

/* Stil für Tabellenzellen */
th,
td {
  font-size: 18px;
  /* Schriftgröße */
}

/* Stil für Tabellenzellen im td-Tag */
td {
  text-align: right;
  /* Textausrichtung */
}

/* Stil für Tabellenzeilen beim Hover */
table tr:hover {
  color: red;
  /* Textfarbe beim Hover */
}

/* Stil für den Button zum Ändern des Ortes */
.change-btn {
  background-image: linear-gradient(to right, rgb(0, 91, 210), rgb(224, 0, 224));
  /* Farbverlauf für den Button */
  color: #ffffff;
  /* Textfarbe */
}
</style>
