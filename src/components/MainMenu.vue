<template>
  <h1>Main menu</h1>
  <button @click="emit('startGame', true)">Start the game!</button>
</template>
<script setup>
const emit = defineEmits(["startGame"]);
</script>
<style>
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
}

h1 {
  font-size: 3em;
}

button {
  padding: 10px 20px;
  font-size: 3em;
}
</style>
