<script setup>
import { ref, onMounted } from "vue";
import { API_URL, API_KEY } from "./constants/index";

//COMPONENTS
import WeatherInfo from "./components/WeatherInfo.vue";

const searchInput = ref("");
const result = ref(null);

//METHODS
function getWeatherInfo() {
  fetch(
    `${API_URL}?q=${searchInput.value}&units=metric&lang=en&appid=${API_KEY}`
  )
    .then((res) => res.json())
    .then((data) => {
      result.value = data;
      console.log(data);
    });
}

onMounted(getWeatherInfo);
</script>

<template>
  <div class="wrapper">
    <form class="weather_search-form" @submit.prevent="getWeatherInfo">
      <input class="weather_search-input" v-model="searchInput" type="text" placeholder="Enter a city..."/>
    </form>
    <!-- WeatherInfo - component -->
    <WeatherInfo :resultInfo="result" /><!-- задаем props с названием resultInfo и в него передаем объект с данными result как значение. т.е. resultInfo - это ключ, а result - значение-->
  </div>
</template>

<style>

@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Poppins', sans-serif;
}

.wrapper {
  background: #0F2027;
  /* fallback for old browsers */
  background: -webkit-linear-gradient(to right, #2C5364, #203A43, #0F2027);
  /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(to right, #2C5364, #203A43, #0F2027);
  /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  min-height: 100vh;
}

.weather_search-form {
  margin-bottom: 10px;
  padding: 5px 10px;
  border-radius: 10px;
  background-color: #fff;
  width: 200px;
}

input.weather_search-input {
  border: none;
  outline: none;
  
  width: 100%;
  color: #2C5364;
}
input.weather_search-input:focus {
  font-weight: 600;
  color: #0F2027;
}

</style>