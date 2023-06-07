<script setup>
  import {ref} from 'vue'

  const player = ref(false);
  const playerComplete = ref(false);
  const host = ref(false);
  const hostComplete = ref(false);
  const playerName = ref('');
  const playerNumber = ref(0);

  function kau() {
    console.log(playerName.value)
    console.log(playerNumber.value)
  }

</script>

<template>
  <div v-if="!player&&!host">
    <h1>Kim jesteś?</h1>
    <button @click="player=!player">Graczem</button>
    <button @click="host=!host">Prowadzącym</button>
  </div>

  <div v-if="player&&!playerComplete">
    <h1>Podaj swoje imię i numer stanowiska</h1>
    <input v-model="playerName" type="text" placeholder="imie">
    <input v-model="playerNumber" type="number" placeholder="numer">
    <button @click="playerComplete=!playerComplete">Gotowe</button>
  </div>

  <div v-if="host">
    <h1>Jak jesteś taki cwany to podaj hasło:</h1>
    <input type="text" name="" id="">
  </div>

  <div class="playerholder" v-if="playerComplete">
    <div class="chanceholder">
      <div class="chance" @click=""></div>
      <div class="chance" @click=""></div>
      <div class="chance" @click=""></div>
    </div>
    <h1>{{playerName}}</h1>
    <h1>{{playerNumber}}</h1>
  </div>
</template>

<style scoped>

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
