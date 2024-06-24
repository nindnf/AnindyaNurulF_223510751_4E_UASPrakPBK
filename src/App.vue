<template>
  <q-layout view="lHh lpr lFf">
    <q-header elevated class="custom-header animated-header">
      <q-toolbar>
        <q-btn flat round dense icon="assignment_ind" class="custom-icon" @click="navigateToLink('https://www.instagram.com/anin_dyarf?igsh=MXRrYW16dDZraDRyYg==')" />
        <q-space />
        <q-toolbar-title class="custom-title">WEATHER</q-toolbar-title>
        <q-space />
        <q-btn-dropdown flat class="custom-btn" label="TUGAS ANIN">
          <q-list>
            <q-item clickable @click="navigateToLink('https://anindyanurul-223510751.vercel.app')">
              <q-item-section>
                TUGAS 1
              </q-item-section>
            </q-item>
            <q-item clickable @click="navigateToLink('https://anindyanurulf-223510751-4-e-t2-prakpbk.vercel.app')">
              <q-item-section>
                TUGAS 2
              </q-item-section>
            </q-item>
            <q-item clickable @click="navigateToLink('https://anindyanurulf-223510751-t3-prak-pbk.vercel.app')">
              <q-item-section>
                TUGAS 3
              </q-item-section>
            </q-item>
            <q-item clickable @click="navigateToLink('https://anindyanurulf-223510751-t4-prak-pbk.vercel.app')">
              <q-item-section>
                TUGAS 4
              </q-item-section>
            </q-item>
            <q-item clickable @click="navigateToLink('https://anindyanurulf-223510751-t5-prak-pbk.vercel.app')">
              <q-item-section>
                TUGAS 5
              </q-item-section>
            </q-item>
            <q-item clickable @click="navigateToLink('https://anindyanurulf-223510751-t6-prak-pbk.vercel.app')">
              <q-item-section>
                TUGAS 6
              </q-item-section>
            </q-item>
            <q-item clickable @click="navigateToLink('')">
              <q-item-section>
                TUGAS 7
              </q-item-section>
            </q-item>
          </q-list>
        </q-btn-dropdown>
        <q-space style="margin-right: 8px;" />
        <q-btn flat round dense icon="sim_card" class="custom-icon" />
        <q-btn flat round dense icon="gamepad" class="custom-icon" />
      </q-toolbar>
    </q-header>

    <q-page-container class="custom-page-container">
      <q-page class="custom-page">
        <Weather :apiKey="apiKey" />
      </q-page>
    </q-page-container>
  </q-layout>
</template>

<script>
import { ref } from 'vue';
import Weather from './views/Weather.vue';

export default {
  name: 'App',
  components: {
    Weather,
  },
  data() {
    return {
      apiKey: 'eef5826d452d04789ef4a8d75e7a42a3',
    };
  },
  methods: {
    navigateToLink(url) {
      window.open(url, '_blank');
    },
  },
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap');

body {
  font-family: 'Roboto', sans-serif;
  background-color: #f5f7fa;
  margin: 0;
  padding: 0;
  height: 100vh;
}

.custom-header {
  background: linear-gradient(135deg, #3c4566, #2848c7) !important;
  border-bottom: 2px solid #ff0000;
  height: 80px; 
  perspective: 1000px; 
  overflow: hidden;
}

.animated-header {
  background-size: 400% 400%;
  animation: gradientAnimation 15s ease infinite;
}

@keyframes gradientAnimation {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

.custom-toolbar {
  padding: 0 20px; 
}

.custom-title {
  font-family: 'Roboto', sans-serif;
  font-size: 2rem; 
  font-weight: 800; 
  color: #ffffff; 
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
  margin: 0;
  padding: 10px;
  transition: transform 0.3s ease-in-out;
  transform-style: preserve-3d; 
}

.custom-title:hover {
  transform: rotateY(15deg); 
  text-shadow: 3px 3px 6px rgba(0, 0, 0, 0.4);
}

.custom-btn .q-btn__content {
  color: #ffffff;
  font-weight: 500;
}

.custom-icon {
  color: #ffffff !important;
  transition: background-color 0.3s, color 0.3s;
}

.custom-icon:hover {
  background-color: #cececea3 !important;
  color: #ffffff !important;
}

.custom-page-container {
  background-color: #65b2ff98;
  display: flex;
  flex: 1;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.custom-page {
  position: relative;
  border-radius: 12px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  padding: 20px;
  transition: box-shadow 0.3s;
  max-width: 600px;
  width: 100%;
  background-image: url('.\assets\bgWeather.jpg');
  background-size: 95%;
  background-position: center;
  overflow: hidden;
}

.custom-page::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: hsla(198, 34%, 79%, 0.22);
  z-index: 1;
}

.custom-page > * {
  position: relative;
  z-index: 2;
}

.custom-page:hover {
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.2);
}

.q-btn {
  color: #ffffff;
  border-radius: 50%;
}

.q-btn:hover {
  background-color: #c1beb8;
  color: #ffffff;
}

.shadow-2 {
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
}

.rounded-borders {
  border-radius: 12px;
}
</style>
