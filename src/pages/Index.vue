<template>
  <q-page class="flex column" :class="bgClass">
    <div class="col q-pt-lg q-px-md">
      <q-input
         v-model="text"
         @keyup.enter="getWeatherbySearch"
         placeholder="Search"
         dark borderless>
        <template v-slot:before>
          <q-icon @click="getLocation"
          name="my_location" />
        </template>
        <template v-slot:append>
          <q-btn
          @click="getWeatherbySearch"
          round
          dense
          flat
          icon="search" />
        </template>
      </q-input>
      </div>
      <template v-if="weatherData">
    <div class="col text-white text-center"> <div class="text-h4 text-weight-light">
      {{weatherData.name}}
    </div> <div class="text-h6 text-weight-light"> {{weatherData.weather[0].main}} </div>
    <div class="text-h1 text-weight-thin q-my-lg relative-position"><span>
      {{ Math.round(weatherData.main.temp)}}</span>
    <span class="text-h4 relative-position degree">&deg;C</span></div>
    </div>
    <div class="col text-center">
      <img :src="`http://openweathermap.org/img/wn/${weatherData.weather[0].icon}@2x.png`" alt="image">
    </div>
    </template>
    <template v-else> <div class="col column text-center text-white">
      <div class="col text-h2 text-weight-thin"> Quasar <br> Weather</div>
      </div>
      <q-btn class="col text-white" @click="getLocation" flat>
      <q-icon left size="3em" name="my_location" />
      <div>Find My Location</div>
    </q-btn>
      </template>
    <div class="col skyline">
      </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      search: '',
      weatherData: null,
      lat: null,
      lon: null
      // apiUrl: 'http://api.openweathermap.org/data/2.5/weather',
      // apiKey: '3813eb98379c6a1bf2b19c5df16bf144'
    }
  }
  /* computed: {
    bgClass () {
      if (this.weatherData) {
        if (this.weatherData.weather[0].icon.ends('n')) {
          return 'bg-night'
        } else {
          return 'bg-day'
        }
    }
  }
},
  methods: {
    getLocation () {
      // this.$q.loading.show()
      navigator.geolocation.getCurrentPosition(
        position => {
          console.log('positon: ', position)
          this.lat = position.coords.latitude
          this.lon = position.coords.longitude
          this.getWeatherByCoords()
        }
      )
    },
    getWeatherByCoords () {
      // this.$q.loading.show()
      this.$axios(`${this.apiURL}?lat=${this.lat}&lon=${this.lon}&appid=${this.apiKey}
      &units=metric`).then(response => {
        this.weatherData = response.data
        // this.$q.loading.hide()
      })
    },
    getWeatherbySearch () {
      //  this.$q.loading.show()
      this.$axios(`${this.apiURL}?q=${this.search}&appid=${this.apiKey}
      &units=metric`).then(response => {
        this.weatherData = response.data
        // this.$q.loading.hide()
      })
    }
  } */
}
</script>

<style lang="sass">
.q-page
  background: linear-gradient(to bottom, #373b44, #4286f4)

.degree
  top:-44px

.skyline
  flex: 0 0 100px
  background: url(../statics/2742.jpg)
  background-size: contain
  background-position: center bottom

</style>
