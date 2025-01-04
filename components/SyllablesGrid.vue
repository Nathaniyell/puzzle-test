<template>
  <div class="flex-1">
    <div class="grid grid-cols-4 gap-1">
      <button v-for="(syllable, i) in syllables" :key="i"
              class="py-2 px-1 text-center text-gray-600 border-2 border-gray-200 rounded-lg hover:border-blue-600 hover:text-blue-600 transition-colors">
        {{ syllable }}
      </button>
    </div>
    <div class="mt-8 flex justify-center">
      <button class="bg-blue-600 text-white px-8 py-3 rounded-full hover:bg-blue-700 transition-colors">
        More Puzzles
      </button>
    </div>
  </div>
</template>

<script setup>
defineProps({
  syllables: {
    type: Array,
    required: true
  }
});
</script>