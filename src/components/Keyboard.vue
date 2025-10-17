<template>
  <div class="keyboard">
    <div v-for="(row, rowIndex) in keys" :key="rowIndex" class="row">
      <button v-for="(key, colIndex) in row" :key="colIndex" class="key">
        {{ key }}
      </button>
    </div>
  </div>
</template>
<script setup>
import { ref } from "vue";
const keys = [
  ["q", "w", "e", "r", "t", "y", "u", "i", "o", "p"],
  ["a", "s", "d", "f", "g", "h", "j", "k", "l"],
  ["z", "x", "c", "v", "b", "n", "m"],
];
const prop = defineProps({
  key: String,
});

const activeKey = ref("");

//TODO: Watcher for adding the class for 100ms to the given key
//watch(
//  () => activeKey.value,
//  (newKey) => {
//    if (newKey.length == 1) {
//    }
//  },
//);
</script>
<style scoped>
.keyboard {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 10vh;
}
.key {
  color: rgba(0, 0, 0, 0.5);
  background-color: #323437;
  border: 1px solid yellow;
  font-size: 2.5em;
  padding: 10px;
  margin-left: 10px;
  margin-bottom: 10px;
  width: 50px;
  border-radius: 10px;
}
.active {
}
</style>
