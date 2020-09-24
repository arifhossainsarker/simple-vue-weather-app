<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input
         type="text" 
         class="search-bar" 
         placeholder="search...."
         v-model="query"
         @keypress="fectWeather"
         >
      </div>
      <!-- {{weather}} -->
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{weather.name}}, {{weather.sys.country}}</div>
          <div class="date">{{dateBuilder()}}</div>
        </div>
        <div class="weather-box">
          <div class="temp">{{Math.round(weather.main.temp)}}</div>
          <div class="weather">{{weather.weather[0].main}}</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
// import Home from './components/Home'

export default {
  name: 'App',
  data(){
    return {
      api_key: '10678697c88e7363d5519235bd230389',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }
  },
  methods:{
    fectWeather(e){
      if(e.key == "Enter"){
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then(res=>{
          return res.json();
        }).then(this.setResults);
      }
    },
    setResults(results){
      this.weather = results;
    },
    dateBuilder(){
      let d = new Date();
      let months = ["January", "Febuary", "March", "April", "May", "june", "july", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thusday", "Friday", "Saterday"];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return `${day} ${date} ${month} ${year}`;

    }
  }
  
}
</script>
  
<style>
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  body{
    font-family: 'montserrat', sans-serif;
  }
  #app{
    background-image: url('./assets/cold-bg.jpg');
    background-size: cover;
    background-position: bottom;
    transition: 0.4s;
  }
  main{
    min-height: 100vh;
    padding: 25px;
    background-image: linear-gradient(to bottom, rgba(0,0,0,.25), rgba(0,0,0,.75));
  }

  .search-box{
    width: 100%;
    margin-bottom: 30px;
  }

  .search-box .search-bar{
    display: block;
    width: 100%;
    padding: 15px;
    appearance: none;
    border: none;
    outline: none;
    border-color: rgba(255, 255, 255, 0.4);
    border-radius: 0 16px 0 16px;
    transition: 0.4s;
  }
  .location-box .location{
    color: #fff;
    font-size: 32px;
    font-weight: 500;
    text-align: center;
    text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
  }
  .location-box .date{
    text-align: center;
    font-size: 20px;
    color: #fff;
    font-weight: 500;
  }

  .weather-box{
    text-align: center;
  }

  .weather-box .temp{
    font-size: 100px;
    display: inline-block;
    padding: 10px 25px;
    font-weight: 900;
    text-shadow: 3px 6px rgba(0, 0, 0, .25);
    background-color: rgba(255,255, 255, .25);
    margin: 30px 0;
    box-shadow: 3px 6px rgba(0, 0, 0, .25);
    color: #ffffff;
  }

  .weather-box .weather{
    font-size: 25px;
    color: #fff;
    text-shadow: 3px 6px rgba(0, 0, 0, .25);
  }

</style>
