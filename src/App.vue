<template>
  <MainMenu v-if="!startGame" @startGame="startGame = true" />
  <GameEngine v-else-if="startGame" />
</template>
<script setup>
import { ref } from "vue";
import GameEngine from "./components/GameEngine.vue";
import MainMenu from "./components/MainMenu.vue";
const startGame = ref(false);
</script>
<style scoped></style>
