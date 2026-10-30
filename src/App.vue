<script setup>
import { ref, onMounted } from 'vue'

const message = ref(null)
const error = ref(null)

onMounted(async () => {
  try {
    const res = await fetch(`${import.meta.env.VITE_API_URL}/messages/today`, {
      headers: { Accept: 'application/json' },
    })
    if (!res.ok) throw new Error(`Server said ${res.status}`)
    message.value = await res.json()
  } catch (e) {
    error.value = e.message
  }
})
</script>

<template>
  <pre v-if="message">{{ message }}</pre>
  <p v-else-if="error">Something went wrong: {{ error }}</p>
  <p v-else>Loading...</p>
</template>