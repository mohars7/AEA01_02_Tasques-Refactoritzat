<script setup>
import { ref } from 'vue'

const emit = defineEmits(['afegir'])

const novaTasca = ref('')
const error = ref(false)

const enviar = () => {
  const titol = novaTasca.value.trim()
  if (titol === '') {
    error.value = true
    return
  }
  error.value = false
  emit('afegir', titol)
  novaTasca.value = ''
}
</script>

<template>
  <div>
    <input v-model="novaTasca" placeholder="Escriu una nova tasca" @keyup.enter="enviar" />
    <button @click="enviar">Afegir</button>
    <p v-show="error" class="error">El títol no pot estar buit</p>
  </div>
</template>

<style scoped>
button {
  margin-left: 6px;
}
.error {
  color: red;
}
</style>