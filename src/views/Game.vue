<script setup lang="ts">
import { ref, onMounted } from 'vue'
import ItemComponent from '@/components/Item-component.vue'
import type {GameItem} from "@/interfaces/interfaces";

const winner = ref<string | null>(null)
const isTie = ref<boolean>(false)
const gameOver = ref<boolean>(false)

const currentPlayer = ref('Player 1')
const player1Points = 0
const player2Points = 0

let items = ref([] as GameItem[]);
const uncoveredItems = ref([] as number[])
const counter = ref(0);

const startGame = function () {
  const array = ["1", "1", "2", "2", "3", "3", "4", "4", "5", "5", "6", "6", "7", "7", "8", "8"];
  const shuffled = [] as GameItem[];

  for (let i = 16; i > 0; i--) {
    // Get random number between 0 and 15 using Math.random => that's the index of random element
    const index = Math.floor(Math.random() * i);
    // Get that element from items array and push it to shuffled
    const item = {
      uncovered: false,
      value: array[index]
    } as GameItem;
    shuffled.push(item);
    // Remove that element from the items array;
    array.splice(index, 1)
  }

  counter.value +=1;
  items.value = shuffled;
}

const setPoints = function (player: string) {
  // Assigns points to currentPlayer
}

const nextPlayer = function (player: string) {
  // Assigns points to currentPlayer
}

const checkGameOver = function () {
  // Checks if there are some unmatched items or if there's less than 8 points
  // If game is over, check for tie/winner
}

const reset = function () {
  // Resets game values to start over
}

const uncoverItem = function (index: number) {
  // Change the value of "uncovered" of selected item
  items.value[index].uncovered = true;
  // Then push new item to uncoveredItems
  uncoveredItems.value.push(index);

  // If there are two items in uncoveredItems – compare them
  if (uncoveredItems.value.length === 2) {
    compareItems();
  }
}

const compareItems = function () {
  // Compare uncovered items
  const indexItem1 = uncoveredItems.value[0];
  const indexItem2 = uncoveredItems.value[1];

  const item1 = items.value[indexItem1].value;
  const item2 = items.value[indexItem2].value;
  const match = item1 === item2;
  if (match) {
    // If they are the same then:
    // currentPlayer gets a point and plays again
    setPoints(currentPlayer.value as string);
    // The cards should remain uncovered // TODO: take the cards away from the board
    // Check for game over
    checkGameOver();
  }
}

const nextRound = function () {
  nextPlayer(currentPlayer.value as string);
  // The cards are covered again
  const indexItem1 = uncoveredItems.value[0];
  const indexItem2 = uncoveredItems.value[1];
  console.log("uncoveredItems", uncoveredItems.value)

  console.log("indexItem1", indexItem1)

  items.value[indexItem1].uncovered = false;
  items.value[indexItem2].uncovered = false;
  uncoveredItems.value = [];
}

onMounted( () => {
  startGame();
});
</script>

<template>
<div class="game__container">
  <h1>MEMO</h1>
  <p v-if="gameOver">
    Game over! <span v-if="isTie">It is a tie!</span>
    <span v-else-if="winner">{{ winner }} won!</span>
  </p>
  <p v-else>Now playing: {{ currentPlayer }}</p>
  <button class="button" @click="nextRound">Next player!</button>
  <div class="game">
    <div v-for="(item, index) in items" class="item">
      <item-component :key="index" :sign="item.value" :uncovered="item.uncovered" @click="uncoverItem(index)"/>
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
  @apply text-base mt-10;
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
  @apply border-0 rounded-full px-8 py-4 my-10 text-base cursor-pointer;
  background-color: #228cdb;
  color: #170a1c;
}
</style>
