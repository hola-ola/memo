<script setup lang="ts">
import { ref, reactive, computed } from 'vue'
import ItemComponent from '@/components/Item-component.vue'

const winner = ref<string | null>(null)
const isTie = ref<boolean>(false)
const gameOver = ref<boolean>(false)

const currentPlayer = ref('Player 1')
const player1Points = 0
const player2Points = 0

let items = [1, 1, 2, 2, 3, 3, 4, 4, 5, 5, 6, 6, 7, 7, 8, 8];
const itemOne = ref(null)
const itemTwo = ref(null)
const counter = ref(0);

const startGame = function () {
  console.log("startGame")
  // Shuffle the items array
  const copyItems = [...items];
  const shuffled = [];

  for (let i = 16; i > 0; i--) {
    // Get random number between 0 and 15 using Math.random => that's the index of random element
    const index = Math.floor(Math.random() * 15+1);
    // Get that element from items array and push it to shuffled
    shuffled.push(items[index]);
    // Remove that element from the items array;
    copyItems.splice(index, 1)
  }
  console.log("shuffled", shuffled)
  counter.value +=1;
  items = shuffled;
}

const compareItems = function () {
  // Compare itemOne and item2
  // If they are the same then currentPlayer gets a point and plays again
  // If they are different then currentPlayer gets no point and it's other player turn
}

const setPoints = function () {
  // Assigns points to currentPlayer
}

const checkGameOver = function () {
  // Checks if there are some unmatched items or if there's less than 8 points
  // If game is over, check for tie
  // If game is not over, currentPlayer switches
}

const reset = function () {
  // Resets game values to start over
}

const startPlaying = function () {
  // Submits players' names and sets current player
}

const view = function () {
  // Views items value
}
</script>

<template>
<div class="game__container">
  <h1>MEMO</h1>
  <p v-if="gameOver">
    Game over! <span v-if="isTie">It is a tie!</span>
    <span v-else-if="winner">{{ winner }} won!</span>
  </p>
  <p v-else>Now playing: {{ currentPlayer }}</p>
  {{ items }}
  <div class="game">
    <div v-for="(item, index) in items" class="item">
      <item-component :key="index" :sign="item" @click="view" />
    </div>
  </div>

  <button class="button" @click="startGame">Shuffle!</button>
</div>
</template>

<style lang="scss" scoped>
h1 {
  @apply text-8xl;
}

p {
  @apply text-base my-10;
  color: #0b7189;
}
.game {
  @apply grid grid-cols-4 grid-rows-4 gap-3;

  .item {
    @apply h-36 w-36;
    background-color: #0b7189;
  }

  &__container {
    @apply flex flex-col text-center;
  }
}
.button {
  @apply border-0 rounded-full px-8 py-4 mt-10 text-base;
  background-color: #228cdb;
  color: #170a1c;
}
</style>
