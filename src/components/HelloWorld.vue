<template>
  <div class="aztro">
    <div class="left-section">
      <h1 id="aztro-title">{{ msg }}</h1>
      <p id="aztro-description">
        Get daily horoscope!
      </p>

      <h3>Select the date</h3>
      <select v-model="day" name="day" class="day-selector">
        <option disabled selected>day</option>
        <option value="yesterday">YESTERDAY</option>
        <option value="today">TODAY</option>
        <option value="tomorrow">TOMORROW</option>
      </select>

      

      <select v-model="sign" name="sign" class="sign-selector">
        <option disabled selected>sign</option>
        <option value="capricorn">CAPRICORN</option>
        <option value="aquarius">AQUARIUS</option>
        <option value="pisces">PISCES</option>
        <option value="aries">ARIES</option>
        <option value="taurus">TAURUS</option>
        <option value="gemini">GEMINI</option>
        <option value="cancer">CANCER</option>
        <option value="leo">LEO</option>
        <option value="virgo">VIRGO</option>
        <option value="libra">LIBRA</option>
        <option value="scorpio">SCORPIO</option>
        <option value="sagittarius">SAGITTARIUS</option>
      </select>

      <p>day: {{ day }}</p>
      <p>sign: {{ sign }}</p>

      <button @click="getHoroscope">GET HOROSCOPE</button>

    </div>
    
    <div class="right-section">
      <ul id="aztro-result">
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
    getHoroscope: function () {

      url = BASE_URL + '?sign=' + this.sign + '&day=' + this.day;

      axios.post(url).then((response) => {
            this.data = response.data
        })
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.aztro {
  margin-top: 60px;
}

#aztro-title {
  font-size: 50px;
  margin-bottom: 10px;
  font-family: 'Raleway', sans-serif;
}

#aztro-description {
  font-size: 16px;
  margin-top: 5px;
  font-family: 'Raleway', sans-serif;
}

.left-section {
  float: left;
  width: 55%;
  border: medium dashed green;
  padding: 8px;
}

.right-section {
  float: right;
  width: 40%;
  border: medium dashed green;
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
