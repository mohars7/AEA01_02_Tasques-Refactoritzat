<script setup>
defineProps({
  tasca: {
    type: Object,
    required: true,
    validator: (t) => 'id' in t && 'titol' in t && 'completada' in t,
  },
})

const emit = defineEmits(['canviar-estat', 'eliminar'])
</script>

<template>
  <li>
    <span :class="{ completada: tasca.completada }">{{ tasca.titol }}</span>
    <small> ({{ tasca.data }})</small>
    <button @click="emit('canviar-estat', tasca.id)">
      {{ tasca.completada ? 'Desmarcar' : 'Completar' }}
    </button>
    <button @click="emit('eliminar', tasca.id)">🗑️</button>
  </li>
</template>

<style scoped>
li {
  margin: 6px 0;
}
button {
  margin-left: 6px;
}
.completada {
  text-decoration: line-through;
  color: gray;
}
</style>