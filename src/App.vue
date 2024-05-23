<template>
  <div class="app">
    <div class="header container h-100 p-5">
      <h1 class="mb-5">Breeze Wetter</h1>
      <div class="d-flex justify-content-center h-100">
        <div class="searchbar w-50 mx-2">
          <input type="text" class="input form-control" v-model="city" placeholder="Suche nach einer Stadt...">
        </div>
        <button class="btn-search btn btn-primary" @click="searchWeather">
          <i class="fas fa-search"></i> Suche
        </button>
      </div>
    </div>
    <br>
    <Weather :city="city" v-if="showWeather"></Weather>
  </div>
</template>


<script>
// import axios from "axios";
// import { resolve } from 'core-js/fn/promise';
import Weather from './components/weather.vue';


export default (await import('vue')).defineComponent({
  name: 'App',
  components: {
    Weather
  },
  data() {
    return {
      city: '',
      showWeather: false,
    }
  },
  methods: {
    async searchWeather() {
      this.showWeather = false;
      await new Promise(resolve => setTimeout(resolve, 0));
      // await this.$nextTick.Tick();
      this.showWeather = true;
    }
  }
})
</script>

<style>
body {
  background-color: #181818 !important;
}

.header {
  background-color: #2a3038;
  border-radius: 30px;
  color: #ffffff;
  text-align: center;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  margin-top: 1rem;
}


.btn-search {
  background-image: linear-gradient(to right, rgb(0, 91, 210), rgb(224, 0, 224))
}
</style>
