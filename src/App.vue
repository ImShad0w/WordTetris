<template>
  <GameEngine v-if="startGame" />
  <Keyboard v-if="startGame" />
  <MainMenu v-else @gameStart="handleGameStart" />
</template>
<script setup>
import { ref } from "vue";
const startGame = ref(false);
import GameEngine from "./components/GameEngine.vue";
import MainMenu from "./components/MainMenu.vue";
import Keyboard from "./components/Keyboard.vue";
function handleGameStart() {
  startGame.value = true;
}
</script>
<style>
body {
  background-color: #323437;
  font-size: sans-serif;
}
</style>
