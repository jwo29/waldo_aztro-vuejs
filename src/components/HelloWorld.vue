<template>
  <div class="aztro">
    <div class="left-section">

      <div class="title-section">

        <h1 id="aztro-title">{{ msg }}</h1>
        <p id="aztro-description">
          Get daily horoscope!
        </p>
      </div>

      <br/>

      <div class="select-section">

        <!-- 날짜 선택 -->
        <select v-model="day" name="day" class="day-selector">
          <option disabled selected>DAY 📆</option>
          <option value="Yesterday">YESTERDAY</option>
          <option value="Today">TODAY</option>
          <option value="Tomorrow">TOMORROW</option>
        </select>      
        
        <!-- 별자리 선택 -->
        <span>SIGN : </span>
        <select v-model="sign" name="sign" class="sign-selector">
          <option disabled selected>SIGN 🎇</option>
          <option value="Capricorn">CAPRICORN</option>
          <option value="Aquarius">AQUARIUS</option>
          <option value="Pisces">PISCES</option>
          <option value="Aries">ARIES</option>
          <option value="Taurus">TAURUS</option>
          <option value="Gemini">GEMINI</option>
          <option value="Cancer">CANCER</option>
          <option value="Leo">LEO</option>
          <option value="Virgo">VIRGO</option>
          <option value="Libra">LIBRA</option>
          <option value="Scorpio">SCORPIO</option>
          <option value="Sagittarius">SAGITTARIUS</option>
        </select>
      </div>
      <br/>
      <button @click="getHoroscope">GET HOROSCOPE</button>
    
    </div>
    
    <div class="right-section">

      <h3>{{ requestDay }} horoscope for {{ requestSign }}</h3>
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
      requestDay: 'Today',
      requestSign: 'Aries',
      day: 'Today',
      sign: 'Aries'      
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
      this.requestDay = this.day;
      this.requestSign = this.sign;

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

.aztro-main-img {
  widows: 300px;
  height: 300px;
  float: left;
}

.title-section {
  margin: 0 72px 0 16px;
  width: 300px;
  height: 300px;
  float: left;
}

#aztro-title {
  font-size: 50px;
  margin: 10px 10px 10px 0;
  font-family: 'Raleway', sans-serif;
}

#aztro-description {
  font-size: 16px;
  font-family: 'Raleway', sans-serif;
}

.select-section {
  display: inline;
}

.left-section {
  float: left;
  width: 50%;
  border: medium dashed green;
  padding: 12px;
}

.right-section {
  float: right;
  width: 40%;
  border: medium dashed green;
  padding: 8px;
}

select {
  width: 120px;
  height: 30px;
  padding: 5px 30px 5px 10px;
  border-radius: 4px;
  margin-right: 8px;
}

button {
  margin-top: 36px;
  width: 180px;
  height: 40px;
  border-radius: 6px;
  border: 0.5 solid gray;
}


h3 {
  margin: 40px  0;
  text-align: center;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin: 0 10px 8px;
}
a {
  color: #42b983;
}
</style>
