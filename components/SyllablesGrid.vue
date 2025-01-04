<template>
  <div class="flex-1">
    <div class="grid grid-cols-4 gap-1 relative">
      <TransitionGroup name="shuffle">
        <button v-for="item in displaySyllables" :key="item.syllable" :class="[
          'py-2 px-1 text-center rounded-lg',
          item.solved
            ? 'border-blue-600 border-2'
            : 'text-gray-600 border-2 border-gray-200 hover:border-blue-600 hover:text-blue-600'
        ]">
          {{ item.syllable }}
        </button>
      </TransitionGroup>
    </div>
    <div class="mt-8 flex justify-center gap-4">
      <button @click="shuffleSyllables" :disabled="isAllSolved" :class="[
        'px-8 py-3 rounded-md transition-colors',
        isAllSolved
          ? 'bg-gray-300 text-gray-500 cursor-not-allowed'
          : 'bg-stone-300 text-black hover:bg-stone-400'
      ]">
        Shuffle
      </button>
      <button @click="solvePuzzle" :disabled="isAllSolved" :class="[
        'px-8 py-3 rounded-md transition-colors',
        isAllSolved
          ? 'bg-gray-300 text-gray-500 cursor-not-allowed'
          : 'bg-stone-300 text-black hover:bg-stone-400'
      ]">
        Solve
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
  },
  solutions: {
    type: Array,
    required: true
  }
});

const currentSolutionIndex = ref(0);
const syllableStates = ref(props.syllables.map(syllable => ({
  syllable,
  solved: false,
  wordIndex: -1,
  syllableIndex: -1
})));

const isAllSolved = computed(() => currentSolutionIndex.value >= props.solutions.length);

const displaySyllables = computed(() => {
  return [...syllableStates.value].sort((a, b) => {
    if (a.solved && !b.solved) return 1;
    if (!a.solved && b.solved) return -1;
    if (a.solved && b.solved) {
      if (a.wordIndex !== b.wordIndex) {
        return b.wordIndex - a.wordIndex;
      }
      return a.syllableIndex - b.syllableIndex;
    }
    return 0;
  });
});

const shuffleSyllables = () => {
  const unsolvedSyllables = syllableStates.value.filter(s => !s.solved);
  const solvedSyllables = syllableStates.value.filter(s => s.solved);

  syllableStates.value = [
    ...unsolvedSyllables.sort(() => Math.random() - 0.5),
    ...solvedSyllables
  ];
};

const solvePuzzle = () => {
  if (currentSolutionIndex.value >= props.solutions.length) return;

  const solution = props.solutions[currentSolutionIndex.value];

  solution.syllables.forEach((syllable, index) => {
    const syllableState = syllableStates.value.find(s => s.syllable === syllable);
    if (syllableState) {
      syllableState.solved = true;
      syllableState.wordIndex = currentSolutionIndex.value;
      syllableState.syllableIndex = index;
    }
  });

  currentSolutionIndex.value++;
  shuffleSyllables();
};

shuffleSyllables();
</script>

<style scoped>
.shuffle-move {
  transition: all 0.5s ease;
}
</style>