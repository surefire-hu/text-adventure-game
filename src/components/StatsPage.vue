<template>
  <div class="stats-page">
    <div class="equipment-column">
      <h3>Equipaggiamento</h3>
      <p>Armatura: {{ player.equippedItems.armor ? player.equippedItems.armor.name : 'Nessuna' }}</p>
      <p>Arma: {{ player.equippedItems.weapon ? player.equippedItems.weapon.name : 'Nessuna' }}</p>
    </div>
    <div class="stats-column">
      <h2>Statistiche di {{ player.name }}</h2>
      <div class="stats">
        <p>Forza: {{ player.stats.forza }}</p>
        <p>Difesa: {{ player.stats.difesa }}</p>
        <p>Velocità: {{ player.stats.velocità }}</p>
      </div>
      <button @click="startAdventure" class="start-adventure-btn">Inizia Avventura</button>
    </div>
    <div class="inventory-column">
      <h3>Inventario</h3>
      <ul>
        <li v-for="item in player.inventory" :key="item.id">
          {{ item.name }}
          <button v-if="item.type === 'armor' || item.type === 'weapon'" @click="equipItem(item)">Equipaggia</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'

defineProps(['player'])
const emits = defineEmits(['start-adventure', 'equip-item'])

function equipItem(item) {
  emits('equip-item', item)
}

function startAdventure() {
  emits('start-adventure')
}
</script>

<style scoped>

.stats-page {
  display: flex;
  background-color: #ffffff;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0,0,0,0.1);
  font-family: Arial, sans-serif;
  height: 600px;
}

.equipment-column, .stats-column, .inventory-column {
  flex: 1;
  padding: 20px;
}

.equipment-column {
  background-color: #ffffff;
  border-radius: 10px 0 0 10px;
}

.stats-column {
  border-left: 1px solid #ccc;
  border-right: 1px solid #ccc;
}

.inventory-column {
  background-color: #ffffff;
  border-radius: 0 10px 10px 0;
}

h2, h3 {
  color: #3815c6;
  margin-top: 0;
}

.stats {
  margin-bottom: 20px;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin-bottom: 10px;
  background-color: #ffffff;
  padding: 10px;
  border-radius: 5px;
}

button {
  background-color: #4CAF50;
  border: none;
  color: white;
  padding: 5px 10px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 14px;
  cursor: pointer;
  border-radius: 3px;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #45a049;
}

.start-adventure-btn {
  display: block;
  width: 100%;
  padding: 10px;
  font-size: 16px;
  margin-top: 60px;
}
</style>
