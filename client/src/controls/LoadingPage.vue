<template>
  <div class="flex flex-col items-center justify-center h-screen w-full bg-black text-white font-sans">
    <!-- Spinner Icon -->
    <div
      class="w-16 h-16 border-4 border-white border-t-transparent rounded-full animate-spin"
      :class="spinClass"
    ></div>

    <!-- Player Count -->
    <p class="mt-6 text-lg tracking-wide">
      {{ currentPlayers }} / {{ maxPlayers }} players joined
    </p>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

// placeholders for now
const currentPlayers = ref(1) 
const maxPlayers = ref(4)

// For triggering periodic spin restart
const spinClass = ref('')
let intervalId: number | undefined

onMounted(() => {
  // Restart spin animation every 3 seconds
  intervalId = window.setInterval(() => {
    spinClass.value = 'animate-none' // temporarily stop animation
    void spinClass.value // force reflow
    setTimeout(() => {
      spinClass.value = '' // reapply spin
    }, 10)
  }, 3000)
})

onUnmounted(() => {
  clearInterval(intervalId)
})
</script>

<style scoped>
/* Custom Tailwind spin animation override (optional) */
@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}

.animate-spin {
  animation: spin 1s linear infinite;
}
</style>
