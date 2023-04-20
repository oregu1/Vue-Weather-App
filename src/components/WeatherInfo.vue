<script setup>
import { cappitalizeFirstLetter } from '../utils';

const props = defineProps({
    resultInfo: {
        type: [Object, null],
        required: true,
    },
});

const today = new Date().toLocaleString('en-EN', { weekday: 'short', year: 'numeric', month: 'long', day: 'numeric' })
</script>
<template>
    <!-- Отрисовываем компонент если в нашем объекте props есть раздел weather -->
    <!-- render a component if there is the weather as a props-item -->
    <div v-if="resultInfo?.name" class="weather-section">
        <div class="weather-icon">
            <img :src="`/src/assets/img/${resultInfo?.weather[0]?.description}.png`" alt="" />
        </div>
        <div class="weather-description">
            {{ cappitalizeFirstLetter(resultInfo?.weather[0]?.description) }}
        </div>

        <div class="city-info">
            <h1>{{ resultInfo?.name }}</h1>
            <p>{{ resultInfo?.sys?.country }}</p>
        </div>

        <div class="weather-temp">
            {{ Math.round(resultInfo?.main?.temp) }} °C
        </div>

        <div class="date-info">
            {{ today }}
        </div>
    </div>
</template>

<style scoped>
.weather-section {
    background: #141E30;
    /* fallback for old browsers */
    background: -webkit-linear-gradient(to right, #243B55, #141E30);
    /* Chrome 10-25, Safari 5.1-6 */
    background: linear-gradient(to right, #243B55, #141E30);
    /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
    border-radius: 5px;
    max-width: 350px;
    width: 100%;
    padding: 10px;
    color: aliceblue;

    box-shadow: 9px 9px 24px -5px rgba(0, 0, 0, 0.75);
    -webkit-box-shadow: 9px 9px 24px -5px rgba(0, 0, 0, 0.75);
    -moz-box-shadow: 9px 9px 24px -5px rgba(0, 0, 0, 0.75);

    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    text-align: center;

    overflow: hidden;
}

.weather-icon {
    width: 100px;
    height: 100px;
}

.weather-icon img {
    width: 100%;
}
</style>