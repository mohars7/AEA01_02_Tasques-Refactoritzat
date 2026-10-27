<script setup>
import TaskItem from './TaskItem.vue'

defineProps({
  tasques: { type: Array, required: true },
})

defineEmits(['canviar-estat', 'eliminar'])
</script>

<template>
  <ul v-if="tasques.length > 0">
    <TaskItem
      v-for="tasca in tasques"
      :key="tasca.id"
      :tasca="tasca"
      @canviar-estat="$emit('canviar-estat', $event)"
      @eliminar="$emit('eliminar', $event)"
    />
  </ul>
  <p v-else>No hi ha tasques per mostrar</p>
</template>

<style scoped>
ul {
  list-style: none;
  padding: 0;
}
</style>