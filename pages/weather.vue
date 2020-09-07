<template>
  <div id="app">
    <!-- ---------------------Search box------------------------- -->
    <div class="b-shadow flex m-5 h-20 p-6 md:mt-10 md:h-16 md:pt-4 rounded-lg text-2xl my-4">
      <img class="h-10 object-contain" src="/location.svg" alt="location" />
      <input
        type="text"
        class="w-full md:mt-1 mx-2 outline-none"
        placeholder="Search..."
        v-model="query"
        @keypress="fetchWeather"
      />
      <div class="flex ml-auto">
        <img class="object-contain h-10" src="/search.svg" alt="search" />
      </div>
    </div>
    <!-- -----------------------------------Horizontal tabs------------------------------------------------ -->
    <div v-if="typeof weather.main != 'undefined'" class="flex m-5 text-2xl text-bold scrolltabs">
      <span>
        <p>{{ dayfeatch() }}</p>
        <p>{{ Math.round(weather.main.temp) }}°c</p>
        <p>
          <img class="m-5 h-10" src="/sunny.svg" alt="search" />
        </p>
        <p>{{ weather.weather[0].main }}</p>
      </span>

      <span>
        <p>{{ dayfeatch() }}</p>
        <p>{{ Math.round(weather.main.temp) }}°c</p>
        <p>
          <img class="m-5 h-10" src="/sunny.svg" alt="search" />
        </p>
        <p>{{ weather.weather[0].main }}</p>
      </span>

      <span>
        <p>{{ dayfeatch() }}</p>
        <p>{{ Math.round(weather.main.temp) }}°c</p>
        <p>
          <img class="m-5 h-10" src="/sunny.svg" alt="search" />
        </p>
        <p>{{ weather.weather[0].main }}</p>
      </span>

      <span>
        <p>{{ dayfeatch() }}</p>
        <p>{{ Math.round(weather.main.temp) }}°c</p>
        <p>
          <img class="m-5 h-10" src="/sunny.svg" alt="search" />
        </p>
        <p>{{ weather.weather[0].main }}</p>
      </span>

      <span>
        <p>{{ dayfeatch() }}</p>
        <p>{{ Math.round(weather.main.temp) }}°c</p>
        <p>
          <img class="m-5 h-10" src="/sunny.svg" alt="search" />
        </p>
        <p>{{ weather.weather[0].main }}</p>
      </span>

      <span>
        <p>{{ dayfeatch() }}</p>
        <p>{{ Math.round(weather.main.temp) }}°c</p>
        <p>
          <img class="m-5 h-10" src="/sunny.svg" alt="search" />
        </p>
        <p>{{ weather.weather[0].main }}</p>
      </span>

      <span>
        <p>{{ dayfeatch() }}</p>
        <p>{{ Math.round(weather.main.temp) }}°c</p>
        <p>
          <img class="m-5 h-10" src="/sunny.svg" alt="search" />
        </p>
        <p>{{ weather.weather[0].main }}</p>
      </span>
    </div>
    <!-- -------------------------------------Summary section------------------------------------------------------ -->
    <!-- ------------first part---------------- -->
    <div class="b-shadow md:mx-10 m-5 p-6 rounded-lg" v-if="typeof weather.main != 'undefined'">
      <div class="flex mx-10">
        <div class="text-6xl font-bold">{{ Math.round(weather.main.temp) }}°c</div>
        <div v-if="weather.main.temp >= 25">
          <img class="mx-10 mt-3 h-20" src="/haze.svg" alt="haze" />
        </div>
        <div v-else-if="weather.main.temp <= 25">
          <img class="mx-10 mt-3 h-20" src="/sunny.svg" alt="sunny" />
        </div>
        <div v-else-if="weather.main.temp <= 15">
          <img class="mx-10 mt-3 h-20" src="/cloudy.svg" alt="cloudy" />
        </div>
      </div>
      <!-- ----------------second part-------------------- -->
      <div class="h-40">barchart</div>

      <div class="flex text-xl font-bold justify-center">
        <div class="w-1/2 mr-3 p-3 bg-blue-100">
          Pressure
          <br />
          {{ weather.main.pressure }} hps
        </div>
        <div class="w-1/2 ml-3 p-3 bg-blue-100">
          Humidity
          <br />
          {{ weather.main.humidity }} %
        </div>
      </div>
      <!-- -----------------------third part------------------------------------- -->
      <div class="flex mt-5 text-xl font-bold justify-center">
        <div class="w-1/2 md:ml-16 p-3">
          Sunrise
          <br />
          {{ Math.round(weather.sys.sunset) }}
        </div>
        <div class="w-1/2 md:ml-32 p-3">
          Sunset
          <br />
          {{ Math.round(weather.sys.sunrise) }}
        </div>
      </div>
      <img class="w-full object-contain" src="/sunset.png" alt="sunset" />
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      api_key: "333936b8790448d4c54576684dd46876",
      url_base: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {},
    };
  },
  methods: {
    fetchWeather(e) {
      if (e.key == "Enter") {
        fetch(
          `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
        )
          .then((res) => {
            return res.json();
          })
          .then(this.setResults);
      }
    },
    setResults(results) {
      this.weather = results;
    },
    dayfeatch() {
      let d = new Date();

      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];
      let day = days[d.getDay()];
      return `${day} `;
    },
  },
};
</script>

<style>
.b-shadow {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
}
@media screen and (max-width: 640px) {
  div.scrolltabs {
    background-color: #ffff;
    overflow: auto;
    white-space: nowrap;
  }

  div.scrolltabs span {
    display: inline-block;
    color: black;
    text-align: center;
    padding: 30px;
    text-decoration: none;
  }

  div.scrolltabs span:hover {
    border-style: solid;
    border-color: blue;
    border-width: 5px;
  }
}

@media screen and (min-width: 650px) {
  div.scrolltabs {
    background-color: #ffff;

    white-space: nowrap;
  }

  div.scrolltabs span {
    color: black;
    text-align: center;
    padding: 45px;
    text-decoration: none;
  }

  div.scrolltabs span:hover {
    border-style: solid;
    border-color: blue;
    border-width: 5px;
  }
}
</style>
