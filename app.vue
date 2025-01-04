<template>
  <div class="min-h-screen bg-gray-100">
    <GameHeader />
    <main class="container mx-auto p-4 mt-8">
      <div class="flex flex-col md:flex-row gap-20">
        <WordList :words="words" />
        <SyllablesGrid :syllables="syllables" />
      </div>
    </main>
  </div>
</template>

<script setup>
const words = [
  { text: 'breath', points: 2 },
  { text: 'breathless', points: 8 },
  { text: 'buffoon', points: 4 },
  { text: 'buffoonery', points: 8 },
  { text: 'buss', points: 2 },
  { text: 'daffodil', points: 4 },
  { text: 'dale', points: 2 },
  { text: 'dance', points: 2 },
  { text: 'dare', points: 2 },
  { text: 'daredevils', points: 8 },
  { text: 'devils', points: 2 },
  { text: 'foils', points: 2 }
];

const syllables = [
  'fo', 'ery', 'tish', 'on',
  'nce', 'et', 'ath', 'tan',
  'ffo', 'le', 'bu', 'per',
  'bre', 'rma', 'ss', 'dil'
];
</script>