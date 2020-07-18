<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 20 ? 'warm' :''">
    <main>
      <div class="text">Weather App</div>
      <div class="search-box">
        <input
          type="text"
          class="search-bar"
          placeholder="Enter Name of State or Country..."
          v-model="query"
          @keypress="fetchWeather"
        />
      </div>
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{weather.name}}, {{weather.sys.country}}</div>
          <div class="date">{{dateBuilder()}}, {{timeBuilder()}} (WAT) </div>
        </div>

        <div class="weather-box">
          <div class="temp">{{Math.round(weather.main.temp)}}°c</div>
          <div class="weather">{{weather.weather[0].main}}</div>
        </div>
        
      </div>
          <div class="foot"> 
            <footer class="footer">Made with ❤️ by <a href="http://github.com/ayodelesalimon">Ayodele Salimonu</a>
            </footer>
            </div>
 
    </main>
  <!-- <div> <footer class="footer">Made with ❤️ by <a href="http://github.com/ayodelesalimon">Ayodele Salimonu</a></footer></div> -->

  </div>
  
</template>

<script>
export default {
  data() {
    return {
      api_key: "63e9e1b46b02ac6c6b4771ee697955e7",
      url_base: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {}
    };
  },
  methods: {
    fetchWeather(e) {
      if (e.key == "Enter") {
        fetch(
          `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
        )
          .then(res => {
            return res.json();
          })
          .then(this.setResults);
      }
    },
    setResults(results) {
      this.weather = results;
    },

    timeBuilder(){
      let d = new Date();
      let hour = d.getHours();
      let minute = d.getMinutes();
      
       return ` ${hour}:${minute}` ;
    },
    dateBuilder() {
      let d = new Date();
      let months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December"
      ];
      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday"
      ];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      

      return `${day} ${date} ${month} ${year} ` ;
    }
  }
};
</script>

<style scoped>
#app {
  background-image: url("../assets/cold.jpg");
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}
#app.warm {
  background-image: url("../assets/hot.jpg");
}
.text{
  text-align: center;
  font-size: 50px;
  color: white;
  font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
  font-style: normal;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
}
main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.25),
    rgba(0, 0, 0, 0.75)
  );
}
.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  border: none;
  background: none;
  background-color: rgba(255, 255, 255, 0.5);
  outline: none;
  appearance: none;
  color: #313131;
  border-radius: 0px 16px 0px 16px;
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  transition: 0.4s;
}
.search-box {
  width: 100%;
  margin-bottom: 30px;
}
.search-box .search-bar:focus {
  box-shadow: 0px 0px 16px;
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0px 16px 0px;
}
.location-box .location {
  padding: 5px;
  color: white;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.location-box .date {
  color: white;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}
.weather-box {
  text-align: center;
}
.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 102px;
  font-weight: 900;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 6px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.weather-box .weather {
  color: white;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;

  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.footer {
    
    text-align: center;
    font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
    font-size: 20px;
    color: white;
}
.footer a{
    text-decoration: none;
    color: white;
    
}
.foot{
   padding: 100px 250px;
}

</style>