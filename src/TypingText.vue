<template>
  <p class="lead mb-4">
    <span>{{ display }}</span
    ><span class="typing-dots">...</span>
  </p>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

const props = defineProps<{ text: string }>()
const display = ref('')

onMounted(() => {
  let i = 0
  const interval = setInterval(() => {
    if (i < props.text.length) {
      display.value += props.text[i]
      i++
    } else {
      clearInterval(interval)
    }
  }, 40)
})
</script>

<style scoped>
.typing-dots {
  animation: blink 1s infinite;
  opacity: 0.6;
}
@keyframes blink {
  0%,
  100% {
    opacity: 0.6;
  }
  50% {
    opacity: 0;
  }
}
</style>
