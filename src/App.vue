<script setup>
import { onMounted, ref } from 'vue';

const inputText = ref('');
const listItems = ref([]);

onMounted(() => {
  initMap();
});

function updateList(event) {
  listItems.value = [event.target.value];
}

function copyToClipboard(url) {
  navigator.clipboard.writeText(url).then(() => {
    alert('Enlace de ubicación copiado al portapapeles');
  });
}

function initMap() {
  const map1 = new google.maps.Map(document.getElementById('map1'), {
    center: { lat: 19.467957773571737, lng: -99.27622669729062 }, 
    zoom: 16,
  });

  const marker1 = new google.maps.Marker({
    position: { lat: 19.467957773571737, lng: -99.27622669729062 },
    map: map1,
    title: 'Lugar 1',
  });

  const map2 = new google.maps.Map(document.getElementById('map2'), {
    center: { lat: 19.463189571452233, lng: -99.28598419584462 }, 
    zoom: 12,
  });

  const marker2 = new google.maps.Marker({
    position: { lat: 19.463189571452233, lng: -99.28598419584462 }, 
    map: map2,
    title: 'Lugar 2',
  });
}

window.initMap = initMap;
</script>

<template>
  <div class="home">
    <img class="home_logo" src="./assets/Boda_preview1.png" alt="logo_boda">
    <!--<input type="text" v-model="inputText" @input="updateList" placeholder="Escribe algo..." />-->
    <ul>
      <li v-for="item in listItems" :key="item">{{ item }}</li>
    </ul>
    <div class="home_header">
      <label>Ubicaciones</label>
      <hr class="separator" />
    </div>
    <div class="home_info">
      <div class="home_info-map">
        <h1 class="home_info-map--title">La misa se llevará a cabo a las <strong>16:00 hrs.</strong> en la Iglesia de San Miguel</h1>
        <div id="map1" class="home_info-map--container"></div>
        <button class="home_info-map--copy" @click="copyToClipboard('https://www.google.com/maps?q=19.467957773571737,-99.27622669729062')">Copiar enlace de ubicación</button>
      </div>
      <div class="home_info-map">
        <h1 class="home_info-map--title">La fiesta se llevará a cabo a las <strong>17:30 hrs.</strong> en:</h1>
        <div id="map2" class="home_info-map--container"></div>
        <button class="home_info-map--copy" @click="copyToClipboard('https://www.google.com/maps?q=19.463189571452233,-99.28598419584462')">Copiar enlace de ubicación</button>
      </div>
    </div>
    
    
  </div>
</template>

<style scoped>
.home {
  display: flex;
  flex-direction: column;  
  justify-content: center;
  padding: 32px 0;
}

.home_logo {
  width: 200px;
  max-width: 300px;
  margin: 0 auto;
}
.home_header {
  font-size: 24px;
  font-weight: bold;
  color: #9e9e9e;
  padding: 0 1rem;
}

.home_info {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 20px;
  padding: 20px;
  box-sizing: border-box;
}

.home_info-map {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.home_info-map--container {
  width: 100%;
  height: 300px;
  border-radius: 10px;
}

.home_info-map--title {
  margin-top: 10px;
  text-align: center;
  font-size: 1.2rem;
  height: 60px;
}

.home_info-map--copy {
  font-family: "Caveat", cursive;
  margin-top: 10px;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  background-color: #b08c03;
  color: #f5f5f5;
  cursor: pointer;
}

@media (min-width: 768px) {
  .home_info {
    flex-direction: row;
    justify-content: space-between;
  }

  .home_info-map--container {
    
  }

  .home_logo {
    width: 280px;
  }

  .home_header {
    padding: 0 3rem;
  }
}
</style>
