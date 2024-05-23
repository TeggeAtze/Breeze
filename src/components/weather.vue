<template>
    <div class="container p-0">
        <div class="d-flex">
            <div class="card main-div w-100">
                <div class="p-3">
                    <h2 class="mb-1 day">Donnerstag</h2>
                    <p class="text-light date mb-0">Datum</p>
                    <small>16:08</small>
                    <h2 class="place">
                        <i class="fas fa-map-marker-alt"></i> Magdeburg <small>Deutschland</small>
                    </h2>
                    <div class="temp">
                        <h1 class="weather-temp">19&deg;</h1>
                        <h2 class="text-light">Beschreibung...</h2>
                    </div>
                </div>
            </div>
            <div class="card card-2 w-100">
                <table class="m-4">
                    <tbody>
                        <tr>
                            <th>Windstärke</th>
                            <td>100</td>
                        </tr>
                        <tr>
                            <th>Feuchtigkeit</th>
                            <td>100</td>
                        </tr>
                        <tr>
                            <th>Regenwahrscheinlichkeit</th>
                            <td>100</td>
                        </tr>
                    </tbody>
                </table>

                <daysWeather></daysWeather>
                <div id="div_Form" class="d-flex m-3 justify-content-center">
                    <form action="">
                        <input type="button" value="Ort ändern" class="btn change-btn btn-primary">
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
    props: {
        city: String,
    },
    data() {
        return {
            weatherData: null
        };
    },
    async created() {
        try {
            const response = await axios.get(`https://api.openweathermap.org/data/3.0/onecall?q=${this.city}&appid=7e9510c437c764a83a929511dc6ee3a3&units=metric`);
            this.weatherData = response.data; // Speichern der erhaltenen Wetterdaten in der Komponentendaten
        } catch (error) {
            console.error(error);
        }
    }
};
</script>


<style>
body {
  background-color: #343d4b;
  color: #ffffff; /* Textfarbe auf der gesamten Seite */
}

.header {
  background-color: #1e2532;
  border-radius: 30px;
}

.btn-search {
  background-image: linear-gradient(to right, rgb(0, 91, 210), rgb(224, 0, 224));
  color: #ffffff; /* Textfarbe für den Button */
}

.weather-temp {
  margin: 0;
  font-weight: 700;
  font-size: 4em;
}

h2.mb-1.day {
  font-size: 3rem;
  font-weight: 400;
}

.main-div {
  border-radius: 30px;
  background-image: url("https://www.capetownetc.com/wp-content/uploads/2022/09/pexels-jonathan-petersson-1237119-1024x681.jpg");
  background-size: cover;
  background-position: center;
  background-blend-mode: overlay;
  background-color: rgba(0, 0, 0, 0.301);
  background-repeat: no-repeat;
  min-height: 300px; /* Mindesthöhe für die Hauptkarte */
  position: relative; /* Damit das Kind-Element .temp richtig positioniert wird */
  color: #ffffff; /* Textfarbe für die Hauptkarte */
}

.temp {
  position: absolute;
  bottom: 10px; /* Abstand von unten */
  left: 10px; /* Abstand von links */
}

.main-div:hover {
  transform: scale(1.1);
  transition: transform 0.8s ease-in-out;
  z-index: 1;
}

.card-2 {
  background-color: #242b34;
  border-radius: 30px;
  color: #ffffff; /* Textfarbe für die Karte */
  min-height: 200px; /* Mindesthöhe für die zweite Karte */
  margin-left: 1.5rem;
}

.card-details {
  margin-left: 19px;
}

.h1_left {
  position: absolute;
  bottom: 25px;
  left: 16px;
  font-size: 3vw;
  line-height: 1.2;
}

.h3_left {
  position: absolute;
  left: 16px;
  font-size: 2vw;
  line-height: 0.5;
}

.h3_left small {
  font-size: 1rem;
}

table {
  border-collapse: separate;
  border-spacing: 15px;
  width: 85%;
  text-align: left;
  max-width: 600px;
  margin: 0 auto;
  color: #ffffff; /* Textfarbe für die Tabelle */
}

th,
td {
  font-size: 18px;
}

td {
  text-align: right;
}

table tr:hover {
  color: red;
}

.change-btn {
  background-image: linear-gradient(to right, rgb(0, 91, 210), rgb(224, 0, 224));
  color: #ffffff; /* Textfarbe für den Button */
}
</style>