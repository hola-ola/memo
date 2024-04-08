<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps({
  sign: {
    type: Number,
    default: null
  }
})
</script>

<template>
  <div class="item">
    <p>{{ sign }}</p>
  </div>
</template>

<style scoped>
.item {
  @apply w-full h-full flex flex-row justify-center items-center cursor-pointer;

  p {
    @apply text-8xl;
    color: #170a1c;
  }
}
</style>
