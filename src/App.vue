<script setup>
  import {ref} from 'vue'

  const player = ref(false);
  const playerDataCompleted = ref(false);
  const playerFinal = ref(false);
  const playerFinalDataCompleted = ref(false);

  const password = ref('');
  const idiot = ref(false);

  const host = ref(false);
  const hostComplete = ref(false);

  const playerName = ref('');
  const playerNumber = ref(0);
  const playerPoints = ref(0);

  const isOn1 = ref(true);
  const isOn2 = ref(true);
  const isOn3 = ref(true);

  function activateHost() {
    if(password.value === 'wdupetrzaslo') {
      host.value = false;
      hostComplete.value = true;
      idiot.value = false;
    } else {
      idiot.value = true;
    }
  }

</script>

<template>

  <!-- Menu Główne -->
  <div v-if="!player&&!playerFinal&&!host&&!hostComplete">
    <h1>Kim jesteś?</h1>
    <button @click="player=!player">Graczem</button>
    <button @click="playerFinal=!playerFinal">Graczem w finale</button>
    <button @click="host=!host">Prowadzącym</button>
  </div>

  <!-- Jesteś Graczem -->
  <div v-if="player&&!playerDataCompleted">
    <h1>Podaj swoje imię i numer stanowiska</h1>
    <div class="inputholder">
      <input v-model="playerName" type="text" placeholder="imię">
      <input v-model="playerNumber" type="number">
      <button @click="playerDataCompleted=!playerDataCompleted">Gotowe</button>
    </div>
  </div>
  <!-- Panel Gracza -->
  <div class="playerholder" v-if="playerDataCompleted">
    <div class="chanceholder">
      <div class="chance" :class="{ green: isOn1 }" @touchstart="isOn1=!isOn1"></div>
      <div class="chance" :class="{ green: isOn2 }" @touchstart="isOn2=!isOn2"></div>
      <div class="chance" :class="{ green: isOn3 }" @touchstart="isOn3=!isOn3"></div>
    </div>
    <h1>{{playerName}}</h1>
    <h1>{{playerNumber}}</h1>
  </div>

  <!-- Jesteś Graczen Finałowym -->
  <div v-if="playerFinal&&!playerFinalDataCompleted">
    <h1>Podaj swoje imię i liczbę zachowanych szans z poprzedniego etapu</h1>
    <div class="inputholder">
      <input v-model="playerName" type="text" placeholder="imię">
      <input v-model="playerPoints" type="number">
      <button @click="playerFinalDataCompleted=!playerFinalDataCompleted">Gotowe</button>
    </div>
  </div>

  <!-- Panel Gracza Finałowego -->
  <div class="playerholder" v-if="playerFinalDataCompleted">
    <div class="chanceholder">
      <div class="chance" :class="{ green: isOn1 }" @touchstart="isOn1=!isOn1"></div>
      <div class="chance" :class="{ green: isOn2 }" @touchstart="isOn2=!isOn2"></div>
      <div class="chance" :class="{ green: isOn3 }" @touchstart="isOn3=!isOn3"></div>
    </div>
    <h1>{{playerName}}</h1>
    <h1>{{playerPoints}}</h1>
  </div>

  <!-- Jesteś Prowadzącym -->
  <div v-if="host">
    <h1>Jak jesteś taki cwany to podaj hasło:</h1>
    <div class="inputholder">
      <input type="text" v-model="password" name="" id="">
      <h2 v-if="idiot">Guwniarzu zasrany zajebany</h2>
      <button @click="activateHost">Ok</button>
    </div>
  </div>

  <!-- Panel Prowadzącego -->
  <div v-if="hostComplete">
    <div class="inputholder">
      <iframe width="110" height="110" src="https://www.myinstants.com/instant/1z10-dobrze-8345/embed/" frameborder="0" scrolling="no"></iframe>
      <p>DOBRZE</p>
    </div>
    <div class="inputholder">
      <iframe width="110" height="110" src="https://www.myinstants.com/instant/1z10-zle-81313/embed/" frameborder="0" scrolling="no"></iframe>
      <p>ŹLE</p>
    </div>
    <div class="inputholder">
      <iframe width="110" height="110" src="https://www.myinstants.com/instant/1z10-intro-23781/embed/" frameborder="0" scrolling="no"></iframe>
      <p>PRZERWA</p>
    </div>
    <div class="inputholder"></div>
    <div class="inputholder"></div>
    <div class="inputholder"></div>
    <div class="inputholder"></div>
    <div class="inputholder"></div>


  </div>


</template>

<style scoped>

.inputholder {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.playerholder {
  width: 100%;
  height: 100%;
}
.chanceholder {
  display: flex;
  justify-content: space-around;
  align-items: center;
  top: 0%;
  height: 25%;
  width: 100%;
}
.chance {
  display: flex;
  width: 25%;
  height: 100%;
}

.green {
  background-color: green;
}
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}


</style>
