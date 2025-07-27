<template>
  <div class="min-h-screen bg-gradient-to-b from-pink-100 to-purple-200 flex flex-col items-center justify-evenly p-4">
    <div class="w-full max-w-md text-center">
      <h1 class="text-2xl md:text-4xl font-bold text-pink-700 mb-6">Règles sacrées du couple</h1>
      <ul class="text-sm md:text-base text-gray-700 list-disc list-inside mb-8 space-y-1">
        <li>1. Personne n’élève la voix, on ne parle pas sèchement et on ne se coupe pas la parole.</li>
        <li>2. Ne pas remettre au lendemain les discussions.</li>
        <li>3. Respecter le temps perso de l’autre, ses décisions et ses émotions même si on ne les comprend pas.</li>
        <li>4. On ne dort pas fâchés.</li>
        <li>5. On dit ce qui ne va pas avant que ça explose.</li>
        <li>6. Demander souvent « comment tu te sens dans la relation »</li>
        <li>7. On se rappelle pourquoi on s’est choisis</li>
        <li>8. Croire la personne quand elle dit quelque chose</li>
      </ul>
    </div>

    <div class="relative w-[80vw] max-w-xs aspect-square mb-10">
      <div
        ref="wheel"
        class="absolute inset-0 rounded-full border-4 border-pink-600 bg-pink-300 shadow-lg transition-transform duration-[3000ms] ease-out"
        :style="{ transform: `rotate(${rotation}deg)` }"
      ></div>
      <div
        class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 text-center z-10"
      >
        <button
          @click="spinWheel"
          class="bg-pink-600 hover:bg-pink-700 font-bold py-2 px-6 rounded-full shadow-xl transform transition-transform active:scale-95"
        >
          🎯 Tirer un gage
        </button>
      </div>
      <div class="absolute top-0 left-1/2 transform -translate-x-1/2 w-0 h-0 border-l-[12px] border-r-[12px] border-b-[20px] border-l-transparent border-r-transparent border-b-yellow-400 z-20"></div>
      <!-- Animations festives -->
      <div v-for="n in 5" :key="n" class="absolute rounded-full bg-white/30 blur-xl animate-ping"
        :style="{
          width: `${8 + n * 4}px`,
          height: `${8 + n * 4}px`,
          top: `${Math.random() * 80 + 10}%`,
          left: `${Math.random() * 80 + 10}%`
        }"
      ></div>
    </div>

    <div v-if="result" class="text-center text-lg md:text-xl mt-4 bg-white/80 rounded-lg shadow p-4 w-full max-w-xs animate-fade-in">
      <p class="text-pink-800 font-semibold">💌 Gage :</p>
      <p class="mt-2 text-gray-800">{{ result }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const gages = [
  'Prépare le petit déjeuner ou le déjeuner préféré de l’autre',
  'Faire une corvée que l’autre déteste (vaisselle, poubelle, serpillère…)',
  '10 minutes de silence main dans la main',
  'Offrir une carte-clin valable cette semaine',
  'Servir un petit dej au lit demain matin',
  '1 minute de câlinage sans interruption',
  '30 squats en disant “j’ai eu tort” à voix haute',
  '10 pompes en récitant “j’ai eu tort” à chaque pompe',
  'Tenir en équilibre sur un pied 45s sans tomber',
  '1 minute de chaise contre un mur sans tricher'
]

const result = ref('')
const rotation = ref(0)

const spinWheel = () => {
  const spins = 3 + Math.floor(Math.random() * 3)
  const degree = 360 * spins + Math.floor(Math.random() * 360)
  rotation.value += degree
  setTimeout(() => {
    const selectedIndex = Math.floor(Math.random() * gages.length)
    result.value = gages[selectedIndex]
  }, 3000)
}
</script>

<style scoped>
@keyframes fade-in {
  0% { opacity: 0; transform: scale(0.8); }
  100% { opacity: 1; transform: scale(1); }
}
.animate-fade-in {
  animation: fade-in 0.5s ease-out;
}
</style>