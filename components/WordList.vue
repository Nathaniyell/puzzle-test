<template>
  <div class="bg-white rounded-lg shadow-lg p-6 w-full md:w-1/3">
    <h2 class="text-lg font-semibold mb-4">12 of 25 Words Found</h2>
    <div class="grid grid-cols-2 gap-x-4">
      <div v-for="(column, colIndex) in wordColumns" :key="colIndex" class="space-y-2">
        <div v-for="(word, wordIndex) in column" :key="wordIndex" 
             class="flex justify-between items-center py-2 border-b">
          <span>{{ word.text }}</span>
          <span class="text-blue-600">{{ word.points }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  words: {
    type: Array,
    required: true
  }
});

const wordColumns = computed(() => {
  const midpoint = Math.ceil(props.words.length / 2);
  return [
    props.words.slice(0, midpoint),
    props.words.slice(midpoint)
  ];
});
</script>