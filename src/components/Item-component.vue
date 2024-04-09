<script setup lang="ts">

const props = defineProps({
  sign: {
    type: String,
    default: null
  },
  uncovered: {
    type: Boolean,
    default: false,
  }
})
</script>

<template>
  <div class="item">
    <p v-if="uncovered">{{ sign }}</p>
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
