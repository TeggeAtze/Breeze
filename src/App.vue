<template>
  <!-- Die Hauptvorlage für deine App -->
  <div class="app">
    <!-- Die App-Hauptcontainer -->
    <div class="header container h-100 p-5">
      <!-- Der Header mit dem Titel -->
      <h1 class="mb-5">Breeze Wetter</h1>
      <!-- Ein Suchbereich für Städtenamen -->
      <div class="d-flex justify-content-center h-100">
        <!-- Zentrierte Ausrichtung -->
        <div class="searchbar w-50 mx-2">
          <!-- Sucheingabefeld -->
          <input type="text" class="input form-control" v-model="city" placeholder="Suche nach einer Stadt...">
        </div>
        <!-- Schaltfläche zum Auslösen der Wetterabfrage -->
        <button class="btn-search btn btn-primary" @click="searchWeather">
          <!-- Ein Suchsymbol -->
          <i class="fas fa-search"></i> Suche
        </button>
      </div>
    </div>
    <br>
    <!-- Anzeige des Wetters für die ausgewählte Stadt -->
    <Weather :city="city" v-if="showWeather"></Weather>
  </div>
</template>

<script>
// import axios from "axios";
// import { resolve } from 'core-js/fn/promise';
import Weather from './components/weather.vue';

export default (await import('vue')).defineComponent({
  // Die App-Komponente
  name: 'App',
  // Import des Wetterkomponenten
  components: {
    Weather
  },
  // Daten für die App
  data() {
    return {
      // Die ausgewählte Stadt
      city: '',
      // Steuerung der Anzeige des Wetters
      showWeather: false,
    }
  },
  // Methoden für die App
  methods: {
    // Funktion zum Abrufen des Wetters
    async searchWeather() {
      // Verstecke das Wetter, während es geladen wird
      this.showWeather = false;
      // Warte kurz, bevor das Wetter angezeigt wird
      await new Promise(resolve => setTimeout(resolve, 0));
      // Zeige das Wetter an
      this.showWeather = true;
    }
  }
})
</script>

<style>
/* Stil für den Hintergrund */
body {
  background-color: #181818 !important;
}

/* Stil für den Header */
.header {
  background-color: #2a3038;
  border-radius: 30px;
  color: #ffffff;
  text-align: center;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  margin-top: 1rem;
}

/* Stil für die Suchschaltfläche */
.btn-search {
  background-image: linear-gradient(to right, rgb(0, 91, 210), rgb(224, 0, 224))
}
</style>
