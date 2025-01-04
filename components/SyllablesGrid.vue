<template>
  <div class="flex-1">
    <div class="grid grid-cols-4 gap-1 relative">
      <TransitionGroup name="shuffle">
        <button v-for="syllable in shuffledSyllables" :key="syllable"
          class="py-2 px-1 text-center text-gray-600 border-2 border-gray-200 rounded-lg hover:border-blue-600 hover:text-blue-600">
          {{ syllable }}
        </button>
      </TransitionGroup>
    </div>
    <div class="mt-8 flex justify-center gap-4">
      <button @click="shuffleSyllables"
        class="bg-stone-300 text-black px-8 py-3 rounded-md hover:bg-stone-400 transition-colors">
        Shuffle
      </button>
      <button class="bg-blue-600 text-white px-8 py-3 rounded-full hover:bg-blue-700 transition-colors">
        More Puzzles
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const props = defineProps({
  syllables: {
    type: Array,
    required: true
  }
});

const shuffledSyllables = ref([...props.syllables]);

const shuffleSyllables = () => {
  shuffledSyllables.value = [...shuffledSyllables.value]
    .sort(() => Math.random() - 0.5);
};

shuffleSyllables();
</script>

<style scoped>
.shuffle-move {
  transition: all 0.5s ease;
}
</style>