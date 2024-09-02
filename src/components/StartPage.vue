<template>
  <div class="start-page">
    <h1>Benvenuto all'Avventura Testuale</h1>
    <input v-model="playerName" placeholder="Inserisci il tuo nome">
    <button @click="startGame">Inizia Gioco</button>
  </div>
</template>

<script setup>
import { ref, defineEmits } from 'vue'

const playerName = ref('')
const emit = defineEmits(['start-game'])

function startGame() {
  if (playerName.value.trim()) {
    emit('start-game', playerName.value)
  }
}
</script>

<style scoped>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.start-page {
  max-width: 400px;
  margin: 50px auto;
  padding: 20px;
  background-color: #f0f0f0;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0,0,0,0.1);
  text-align: center;
  font-family: Arial, sans-serif;
}

h1 {
  color: #3815c6;
  margin-bottom: 20px;
}

input {
  width: 100%;
  padding: 10px;
  margin-bottom: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
}

button {
  background-color: #4CAF50;
  border: none;
  color: white;
  padding: 10px 20px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  border-radius: 5px;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #4c45a0;
}
</style>
