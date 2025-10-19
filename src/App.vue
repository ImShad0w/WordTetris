<template>
  <GameEngine v-if="startGame" @activeKey="handleActiveKey" />
  <Keyboard v-if="startGame" :activeKey="currActiveKey" />
  <MainMenu v-else @gameStart="handleGameStart" />
</template>
<script setup>
import { ref } from "vue";
const startGame = ref(false);
const currActiveKey = ref("");

import GameEngine from "./components/GameEngine.vue";
import MainMenu from "./components/MainMenu.vue";
import Keyboard from "./components/Keyboard.vue";

function handleGameStart() {
  startGame.value = true;
}

function handleActiveKey(key) {
  currActiveKey.value = "";
  requestAnimationFrame(() => {
    //Forces vue to detect same key twice
    currActiveKey.value = key;
  });
}
</script>
<style>
body {
  background-color: #323437;
  font-size: sans-serif;
}
</style>
