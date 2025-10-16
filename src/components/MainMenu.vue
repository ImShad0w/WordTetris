<template>
  <div class="container">
    <h1 class="title">Word Tetris</h1>
    <button class="btn-start" @click="emit('gameStart')">
      Start the game!
    </button>
  </div>
</template>
<script setup>
const emit = defineEmits(["gameStart"]);
</script>
<style scoped>
.container {
  width: auto;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.title {
  color: white;
  font-size: 4em;
  font-family: sans-serif;
  margin-top: 30vh;
}

.btn-start {
  color: black;
  background-color: #e2b714;
  padding: 20px 40px;
  font-size: 2em;
  border-radius: 20px;
  border: none;
  cursor: pointer;
}
</style>
