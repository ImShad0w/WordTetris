<template>
  <div class="game-engine">
    <div class="active-word">
      <span
        v-for="(letter, i) in activeWord.text"
        :key="i"
        :class="getLetterClass(i)"
      >
        {{ letter }}
      </span>
    </div>
    <input
      type="text"
      class="word-input"
      v-model="gameState.inputText"
      @input="handleWordInput"
      placeholder="Comença a escriure..."
    />
  </div>
</template>
<script setup>
import { ref, computed, watch } from "vue";

const gameState = ref({
  words: [
    { id: 1, text: "component", state: "pendent" },
    { id: 2, text: "reactivitat", state: "pendent" },
    { id: 3, text: "javascript", state: "pendent" },
    { id: 4, text: "framework", state: "pendent" },
    { id: 5, text: "template", state: "pendent" },
  ],
  activeWordIndex: 0,
  inputText: "",
  stats: [],
  totalErrors: 0,
  currentErrors: 0,
});

const activeWord = computed(() => {
  return gameState.value.words[gameState.value.activeWordIndex];
});

let wordStartTime = 0;

function startWordTimer() {
  wordStartTime = Date.now();
}

function handleWordInput() {
  if (gameState.value.inputText.length === 1 && wordStartTime === 0) {
    startWordTimer();
  }

  if (gameState.value.inputText === activeWord.value.text) {
    const timeTaken = Date.now() - wordStartTime;

    gameState.value.stats.push({
      word: activeWord.value.text,
      time: timeTaken,
      errors: gameState.value.currentErrors,
    });

    gameState.value.currentErrors = 0;
    gameState.value.totalErrors = 0;
    activeWord.value.status = "completed";
    gameState.value.activeWordIndex++;
    gameState.value.inputText = "";
    wordStartTime = 0;

    if (gameState.value.activeWordIndex >= gameState.value.words.length) {
      stopGame();
    }
  }
}

function stopGame() {
  console.log(gameState.value.stats);
}

function getLetterClass(index) {
  const inputText = gameState.value.inputText;
  if (index >= inputText.length) {
    return "";
  }
  if (inputText[index] === activeWord.value.text[index]) {
    return "correct-letter";
  }
  return "incorrect-letter";
}

watch(
  () => gameState.value.inputText,
  (newValue, oldValue) => {
    const target = activeWord.value.text;
    if (newValue.length > oldValue.length) {
      const lastIndex = newValue.length - 1;
      const typedChar = newValue[lastIndex];
      const targetChar = target[lastIndex];
      if (typedChar && typedChar !== targetChar) {
        gameState.value.totalErrors++; // Track mistakes
        gameState.value.currentErrors = gameState.value.totalErrors; // Update currentErrors for stats
      }
    }
  },
);
</script>
<style>
.active-word {
  border: 1px solid black;
}

.correct-letter {
  color: black;
}

.incorrect-letter {
  color: red;
}
</style>
