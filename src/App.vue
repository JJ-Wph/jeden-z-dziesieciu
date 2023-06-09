<template>

  <!-- Menu Główne -->
  <div v-if="!player&&!playerFinal&&!host&&!hostComplete">
    <button @click="toggleFullScreen">Pełny ekran</button>
    <h1>Kim jesteś?</h1>
    <button @click="player=!player">Graczem</button>
    <button @click="playerFinal=!playerFinal">Graczem w finale</button>
    <button @click="host=!host">Prowadzącym</button>
  </div>

  <!-- Jesteś Graczem -->
  <div v-if="player&&!playerDataCompleted">
    <h2>Podaj swoje imię i numer stanowiska</h2>
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
    <h2>Podaj swoje imię i liczbę zachowanych szans z poprzedniego etapu</h2>
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
    <div class="pointsholder">
      <div class="pointsdiv" @touchstart="playerPoints-=10">
      </div>
      <div class="pointsdiv">
        <h1>{{playerName}}</h1>
        <h1>{{playerPoints}}</h1>
      </div>
      <div class="pointsdiv" @touchstart="playerPoints+=10">
      </div>
    </div>
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
    <div class="buttonholder">
      <button style="width: 100px; height: 100px" @click="dobrze.play()">DOBRZE</button>
      <button style="width: 100px; height: 100px" @click="zle.play()">ŹLE</button>
    </div>
    <div class="buttonholder">
      <button style="width: 80px; height: 80px" @click="przerywnik.play()">Brake</button>
      <button style="width: 80px; height: 80px" @click="intro1.play()">Intro1</button>
      <button style="width: 80px; height: 80px" @click="intro2.play()">Intro2</button>
      <button style="width: 80px; height: 80px" @click="intro2.pause()">Intro2 stop</button>
      <button style="width: 80px; height: 80px" @click="adriatica.play()">Zegarki</button>
    </div>

    <button @click="audio1.play()">MUZYCZNE 1</button>
    <button @click="audio2.play()">MUZYCZNE 2</button>
    <button @click="audio3.play()">MUZYCZNE 3</button>
    <button @click="audio4.play()">MUZYCZNE 4</button>
    <button @click="audio5.play()">MUZYCZNE 5</button>
    <button @click="audio6.play()">MUZYCZNE 6</button>
    


  </div>


</template>

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

  const dobrze = new Audio('./src/assets/dobrze.mp3');
  const zle = new Audio('./src/assets/zle.mp3');
  const przerywnik = new Audio('./src/assets/przerywnik.mp3');
  const adriatica = new Audio('./src/assets/adriatica.mp3')
  const intro1 = new Audio('./src/assets/intro1.mp3');
  const intro2 = new Audio('./src/assets/intro2.mp3');

  intro2.playbackRate = 1.25;

  const audio1 = new Audio('./src/assets/pytanie1.mp3');
  const audio2 = new Audio('./src/assets/pytanie2.mp3');
  const audio3 = new Audio('./src/assets/pytanie3.mp3');
  const audio4 = new Audio('./src/assets/pytanie4.mp3');
  const audio5 = new Audio('./src/assets/pytanie5.mp3');
  const audio6 = new Audio('./src/assets/pytanie6.mp3');

  document.documentElement.requestFullscreen();

  function activateHost() {
    if(password.value === 'wdupetrzaslo') {
      host.value = false;
      hostComplete.value = true;
      idiot.value = false;
    } else {
      idiot.value = true;
    }
  }

  function toggleFullScreen() {
    if (!document.fullscreenElement) {
        document.documentElement.requestFullscreen();
    } else {
        document.exitFullscreen();
    }
  }

</script>

<style scoped>

.inputholder, 
.buttonholder, 
.pointsholder {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.buttonholder {
  flex-direction: row;
  margin: 1rem;
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

.pointsholder {
  flex-direction: row;
  height: 75%;
}

.pointsdiv {
  width: 33%;
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
