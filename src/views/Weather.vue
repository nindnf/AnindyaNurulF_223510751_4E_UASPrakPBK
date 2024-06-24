<template>
  <q-card class="my-card q-mt-md">
    <q-card-section>
      <div class="text-h6">Cuaca</div>
      <q-input filled v-model="location" label="Masukkan Lokasi" />
      <q-btn color="primary" label="Cari" @click="getWeather" :loading="loading" />
    </q-card-section>
    <q-card-section v-if="weather && !loading">
      <div class="weather-info">
        <div class="weather-detail">
          <div class="weather-label">Lokasi:</div>
          <div class="weather-value">{{ weather.name }}</div>
        </div>
        <div class="weather-detail">
          <div class="weather-label">Temperatur:</div>
          <div class="weather-value">{{ (weather.main.temp - 273.15).toFixed(2) }}°C</div>
        </div>
        <div class="weather-detail">
          <div class="weather-label">Deskripsi:</div>
          <div class="weather-value">{{ weather.weather[0].description }}</div>
        </div>
      </div>
    </q-card-section>
    <q-card-section v-if="loading" class="loading-section">
      <div>Loading...</div>
    </q-card-section>
    <q-card-section v-if="error" class="error-section">
      <div>Error: {{ error }}</div>
    </q-card-section>
  </q-card>
</template>
  
  <script>
  import { ref } from 'vue';
  import axios from 'axios';
  
  export default {
    name: 'Weather',
    props: {
      apiKey: {
        type: String,
        required: true,
      },
    },
    setup(props) {
      const location = ref('');
      const weather = ref(null);
      const loading = ref(false);
      const error = ref(null);
      const apiUrl = 'https://api.openweathermap.org/data/2.5/weather';
  
      const getWeather = async () => {
        if (!location.value) {
          console.log('Location is empty');
          return;
        }
  
        loading.value = true;
        weather.value = null;
        error.value = null;
        console.log('Fetching weather for:', location.value);
  
        try {
          const response = await axios.get(`${apiUrl}?q=${location.value}&appid=${props.apiKey}`);
          console.log('API response:', response.data);
          weather.value = response.data;
        } catch (err) {
          console.error('Error fetching weather data:', err);
          error.value = 'Error fetching weather data. Please check the API key or location.';
          weather.value = null;
        } finally {
          loading.value = false;
        }
      };
  
      return { location, weather, loading, error, getWeather };
    },
  };
  </script>
  
  <style scoped>
  @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap');
  
  body {
    font-family: 'Roboto', sans-serif;
  }
  
  .my-card {
    max-width: 400px;
    margin: 90px auto;
    padding: 20px;
    background: linear-gradient(135deg, #f5f5f5, #ffffff);
    border-radius: 16px;
    box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s, box-shadow 0.3s;
  }
  
  .my-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 12px 24px rgba(0, 0, 0, 0.2);
  }
  
  .text-h6 {
    font-size: 1.5rem;
    font-weight: bold;
    color: #333;
    text-align: center;
    margin-bottom: 20px;
  }
  
  .my-input {
    margin-bottom: 20px;
  }
  
  .my-button {
    width: 100%;
    margin-top: 10px;
    padding: 12px 20px; 
    font-size: 1rem;
    font-weight: bold;
    color: #ffffff;
    background-color: #007bff; 
    border: none;
    border-radius: 8px;
    cursor: pointer;
    transition: background-color 0.3s, transform 0.2s, box-shadow 0.2s;
  }
  
  .my-button:hover {
    background-color: #0056b3; 
    transform: translateY(-2px); 
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1); 
  }
  
  .weather-info div {
    margin-bottom: 10px;
    font-size: 1.1rem;
  }
  
  .weather-info span {
    font-weight: bold;
    color: #333;
  }
  
  .loading-section {
    text-align: center;
    padding: 20px;
  }
  
  .loading-text {
    margin-top: 10px;
    font-size: 1.1rem;
    color: #666;
  }
  
  .error-section {
    text-align: center;
    padding: 20px;
    background-color: #fdecea;
    border-radius: 8px;
    box-shadow: 0 4px 10px rgba(255, 0, 0, 0.1);
  }
  
  .error-text {
    color: #d32f2f;
    font-size: 1rem;
    font-weight: bold;
  }

  .weather-info {
  margin-top: 20px;
}

.weather-detail {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.weather-label {
  font-weight: bold;
  color: #333;
  width: 100px; 
}

.weather-value {
  font-size: 1.1rem;
  color: #666;
  transition: transform 0.3s ease-in-out; 
}

.weather-value:hover {
  transform: translateX(10px); 
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
}
</style>
  
