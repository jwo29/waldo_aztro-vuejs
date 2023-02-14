<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      Get daily horoscope!
    </p>
    <h3>Select the sign</h3>
    <button @click="getHoroscope('capricorn', this.day)">CAPRICORN</button>
    <button @click="getHoroscope('aquarius', this.day)">AQUARIUS</button>
    <button @click="getHoroscope('pisces', this.day)">PISCES</button>
    <button @click="getHoroscope('aries', this.day)">ARIES</button>
    <button @click="getHoroscope('taurus', this.day)">TAURUS</button>
    <button @click="getHoroscope('gemini', this.day)">GEMINI</button>
    <button @click="getHoroscope('cancer', this.day)">CANCER</button>
    <button @click="getHoroscope('leo', this.day)">LEO</button>
    <button @click="getHoroscope('virgo', this.day)">VIRGO</button>
    <button @click="getHoroscope('libra', this.day)">LIBRA</button>
    <button @click="getHoroscope('scorpio', this.day)">SCORPIO</button>
    <button @click="getHoroscope('sagittarius', this.day)">SAGITTARIUS</button>

    
    <h3>Select the date</h3>
    <button @click="getHoroscope(this.sign, 'yesterday')">YESTER DAY</button>
    <button @click="getHoroscope(this.sign, 'today')">TODAY</button>
    <button @click="getHoroscope(this.sign, 'tomorrow')">TOMORROW</button>
    <ul id="aztro">
      <li>Current Date: {{data.current_date}}</li>
      <li>Compatibility: {{data.compatibility}}</li>
      <li>Lucky Number: {{data.lucky_number}}</li>
      <li>Lucky Time: {{data.lucky_time}}</li>
      <li>Color: {{data.color}}</li>
      <li>Date Range: {{data.date_range}}</li>
      <li>Mood: {{data.mood}}</li>
      <li>Description: {{data.description}}</li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

const BASE_URL = 'https://aztro.sameerkumar.website/';
var url = '';

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data () {
    return {
      data: {},
      sign: 'aries',
      day: 'today'
    }
  },
  created () {
    var url = BASE_URL + '?sign=' + this.sign + '&day=' + this.day;
    axios.post(url).then((response) => {
            this.data = response.data
        })
  },
  methods: {
    getHoroscope: function (sign, day) {

      url = BASE_URL + '?sign=' + sign + '&day=' + day;

      axios.post(url).then((response) => {
            this.data = response.data
        })
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
