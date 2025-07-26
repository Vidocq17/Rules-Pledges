<template>
  <div class="min-h-screen bg-gradient-to-tr from-pink-100 via-sumato-200 to-sumato-100 text-sumato-900 flex flex-col items-center justify-center py-12 px-4">
    <!-- Règles du couple -->
    <div class="w-full max-w-3xl bg-white/80 backdrop-blur-md rounded-3xl shadow-2xl p-8 mb-16 border border-sumato-300">
      <h1 class="text-4xl font-extrabold text-center text-sumato-700 mb-6">💞 Règles du Couple</h1>
      <ul class="list-disc list-inside text-lg leading-relaxed space-y-2">
        <li v-for="(rule, index) in rules" :key="index">{{ rule }}</li>
      </ul>
    </div>

    <!-- Roue et gage -->
    <div class="w-full max-w-md bg-white rounded-3xl shadow-2xl p-10 flex flex-col items-center space-y-6 border border-sumato-300 relative overflow-hidden">
      <h2 class="text-2xl font-bold text-sumato-800 mb-2">🎲 Pioche ton Gage</h2>

      <div class="relative">
        <div
          class="w-52 h-52 rounded-full border-[10px] border-sumato-500 flex items-center justify-center bg-gradient-to-tr from-sumato-100 via-sumato-300 to-sumato-200"
          :class="{ 'spin-animation': isSpinning, 'pulse-glow': !isSpinning }"
        >
          <span class="text-center px-4 text-sumato-800 font-semibold">{{ spinningText }}</span>
        </div>
        <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2">
          <div class="w-4 h-4 bg-sumato-800 rounded-full shadow"></div>
        </div>
        <div v-if="isSpinning" class="absolute inset-0 flex items-center justify-center z-10">
          <div class="confetti"></div>
        </div>
      </div>

      <button
        @click="spinWheel"
        class="bg-gradient-to-r from-sumato-400 to-sumato-600 hover:from-sumato-500 hover:to-sumato-700 text-lg px-8 py-3 rounded-full font-bold transition transform hover:scale-105 shadow-lg"
      >
        🎉 Lancer la roue !
      </button>

      <transition name="fade">
        <div v-if="selectedGage && !isSpinning" class="mt-6 text-center text-xl font-medium text-sumato-900 bg-sumato-100 px-4 py-3 rounded-xl shadow-lg animate-bounce">
          📝 <span class="font-bold">Gage :</span> {{ selectedGage }}
        </div>
      </transition>

      <div class="absolute -top-6 -right-6 w-32 h-32 bg-sumato-300 opacity-30 rounded-full blur-2xl"></div>
      <div class="absolute -bottom-6 -left-6 w-32 h-32 bg-sumato-400 opacity-20 rounded-full blur-2xl"></div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const rules = [
  "Personne n’élève la voix, on ne parle pas sèchement et on ne se coupe pas la parole.",
  "Ne pas remettre au lendemain les discussions.",
  "Respecter le temps perso de l’autre, ses décisions et ses émotions même si on ne les comprend pas.",
  "On ne dort pas fâchés.",
  "On dit ce qui ne va pas avant que ça explose.",
  "Demander souvent « comment tu te sens dans la relation ».",
  "On se rappelle pourquoi on s’est choisis.",
  "Croire la personne quand elle dit quelque chose."
]

const gages = [
  "Préparer le petit déjeuner ou déjeuner préféré de l’autre.",
  "Faire une corvée que l’autre déteste (vaisselle, poubelle, serpillère…).",
  "10 minutes de silence ensemble, main dans la main.",
  "Offrir une carte-câlin valable à tout moment dans la semaine.",
  "Servir le petit-déjeuner au lit le lendemain.",
  "1 minute de gainage.",
  "30 squats en récitant : 'j’ai eu tort'.",
  "10 pompes en disant à chaque fois : 'j’ai eu tort'.",
  "Tenir en équilibre sur un pied pendant 45 secondes (si échec, recommencer).",
  "1 minute de chaise contre le mur."
]

const selectedGage = ref(null)
const spinningText = ref("Clique pour lancer la roue !")
const isSpinning = ref(false)

function spinWheel() {
  isSpinning.value = true
  selectedGage.value = null
  spinningText.value = "🎡 En cours..."

  setTimeout(() => {
    const randomIndex = Math.floor(Math.random() * gages.length)
    selectedGage.value = gages[randomIndex]
    spinningText.value = selectedGage.value
    isSpinning.value = false
  }, 3000)
}
</script>

<style scoped>
@keyframes spin-slow {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(1080deg); }
}
.spin-animation {
  animation: spin-slow 3s cubic-bezier(0.33, 1, 0.68, 1);
}

.pulse-glow {
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0%, 100% { box-shadow: 0 0 0 0 rgba(255, 111, 139, 0.4); }
  50% { box-shadow: 0 0 20px 10px rgba(255, 111, 139, 0.6); }
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s ease;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}

/* Confetti style (optional animation effect placeholder) */
.confetti::before {
  content: '✨';
  font-size: 3rem;
  animation: float 1s ease-in-out infinite;
}
@keyframes float {
  0% { transform: translateY(0); opacity: 1; }
  100% { transform: translateY(-20px); opacity: 0; }
}
</style>
