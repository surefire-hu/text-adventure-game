<template>
  <div id="app">
    <StartPage v-if="currentPage === 'start'" @start-game="startGame" />
    <StatsPage 
      v-else-if="currentPage === 'stats'" 
      :player="player" 
      @toggle-inventory="toggleInventory"
      @start-adventure="startAdventure"
    />
    <GamePage v-else :player="player" :currentScene="currentScene" @make-choice="makeChoice" />
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue'
import StartPage from './components/StartPage.vue'
import StatsPage from './components/StatsPage.vue'
import GamePage from './components/GamePage.vue'

const currentPage = ref('start')
const showInventory = ref(false)

const player = reactive({
  name: '',
  stats: {
    forza: 10,
    difesa: 10,
    velocità: 10
  },
  inventory: [],
  equippedItems: {
    armor: null,
    weapon: null
  }
})

const gameData = reactive({
  scenes: [
    {
      id: 'home',
      description: 'Sei a casa tua. Cosa vuoi fare?',
      choices: [
        { text: 'Esci di casa', nextScene: 'start' },
        { text: 'Controlla le statistiche', action: 'checkStats' }
      ]
    },  
    {
      id: 'start',
      description: "sei davanti ad un incrocio. a sinistra c'è una foresta buia, a destra una montagna alta e imponente.",
      choices: [
        { text: 'entra nella foresta', nextScene: 'forest' },
        { text: 'scalò la montagna', nextScene: 'mountain' }
      ]
    },
    {
      id: 'forest',
      description: 'sei entrato in una foresta buia e spugnosa. senti un odore pungente e il terreno è umido e fangoso.',
      choices: [
        { text: 'continua a camminare', nextScene: 'deepForest' },
        { text: "torna all'incrocio", nextScene: 'start' }
      ]
    },
    {
      id: 'mountain',
      description: "inizi a scalare una montagna alta e ripida. l'aria diventa rarefatta e il respiro si fa difficile.",
      choices: [
        { text: 'continua a scalare', nextScene: 'summit' },
        { text: "torna all'incrocio", nextScene: 'start' }
      ]
    },
    {
      id: 'deepForest',
      description: 'Ti addentri nella foresta profonda. Gli alberi sono così fitti che quasi non passa la luce. Improvvisamente, senti un rumore provenire da un cespuglio vicino.',
      choices: [
        { text: 'Investigare il rumore', nextScene: 'mysteriousCreature' },
        { text: 'Ignorare e continuare', nextScene: 'ancientRuins' },
        { text: 'Tornare indietro', nextScene: 'forest' }
      ]
    },
    {
      id: 'mysteriousCreature',
      description: 'Ti avvicini cautamente al cespuglio. Ne esce una piccola creatura luminosa, simile a una fata. Ti guarda con curiosità.',
      choices: [
        { text: 'Offrire del cibo alla creatura', nextScene: 'fairyFriend' },
        { text: 'Cercare di catturarla', nextScene: 'fairyEscape' },
        { text: 'Lasciarla in pace e continuare', nextScene: 'ancientRuins' }
      ]
    },
    {
      id: 'ancientRuins',
      description: 'Proseguendo nella foresta, ti imbatti in antiche rovine coperte di muschio. Sembrano essere i resti di un tempio dimenticato.',
      choices: [
        { text: 'Esplorare le rovine', nextScene: 'templeInterior' },
        { text: 'Cercare un sentiero intorno', nextScene: 'forestClearing' },
        { text: 'Tornare indietro', nextScene: 'deepForest' }
      ]
    }
  ],
  currentSceneId: 'home'
})

const currentScene = ref(gameData.scenes.find(scene => scene.id === gameData.currentSceneId))

function startGame(name) {
  player.name = name
  currentPage.value = 'stats'
}

function toggleInventory() {
  showInventory.value = !showInventory.value
}

function startAdventure() {
  currentPage.value = 'game'
}

function makeChoice(choiceIndex) {
  const choice = currentScene.value.choices[choiceIndex]
  if (choice.action === 'checkStats') {
    currentPage.value = 'stats'
  } else {
    gameData.currentSceneId = choice.nextScene
    currentScene.value = gameData.scenes.find(scene => scene.id === gameData.currentSceneId)
  }
}
</script>

<style scoped>
.game-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f0f0f0;
  border-radius: 8px;
}

ul {
  list-style-type: none;
  padding: 0;
}

button {
  margin: 5px;
  padding: 10px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}
</style>
