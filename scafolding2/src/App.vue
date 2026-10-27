<script setup>
import { ref, reactive, computed } from 'vue'
import TaskForm from './components/TaskForm.vue'
import TaskList from './components/TaskList.vue'

const tasques = ref([
  { id: 1, titol: 'Tasca 1', completada: true, data: new Date().toLocaleDateString() },
  { id: 2, titol: 'Tasca 2', completada: false, data: new Date().toLocaleDateString() },
  { id: 3, titol: 'Tasca 3', completada: false, data: new Date().toLocaleDateString() },
])
let seguentId = 4

const filtre = reactive({ nomesPendents: false })
const missatge = ref('')
let temporitzador = null

const tasquesVisibles = computed(() =>
  filtre.nomesPendents ? tasques.value.filter((t) => !t.completada) : tasques.value,
)
const total = computed(() => tasques.value.length)
const pendents = computed(() => tasques.value.filter((t) => !t.completada).length)
const completades = computed(() => total.value - pendents.value)

const notificar = (text) => {
  missatge.value = text
  clearTimeout(temporitzador)
  temporitzador = setTimeout(() => (missatge.value = ''), 2500)
}

const afegirTasca = (titol) => {
  tasques.value.push({
    id: seguentId++,
    titol,
    completada: false,
    data: new Date().toLocaleDateString(),
  })
  notificar(`Tasca "${titol}" afegida`)
}

const canviarEstat = (id) => {
  const tasca = tasques.value.find((t) => t.id === id)
  if (!tasca) return
  tasca.completada = !tasca.completada
  notificar(tasca.completada ? 'Tasca completada' : 'Tasca desmarcada')
}

const eliminarTasca = (id) => {
  if (!confirm('Segur que vols eliminar aquesta tasca?')) return
  tasques.value = tasques.value.filter((t) => t.id !== id)
  notificar('Tasca eliminada')
}
</script>

<template>
  <div class="app">
    <h1>Gestor de Tasques</h1>

    <TaskForm @afegir="afegirTasca" />

    <p v-if="missatge" class="notificacio">{{ missatge }}</p>

    <label>
      <input type="checkbox" v-model="filtre.nomesPendents" />
      Mostra només pendents
    </label>

    <TaskList
      :tasques="tasquesVisibles"
      @canviar-estat="canviarEstat"
      @eliminar="eliminarTasca"
    />

    <p>Total: {{ total }} | Pendents: {{ pendents }} | Completades: {{ completades }}</p>
  </div>
</template>

<style scoped>
.app {
  grid-column: 1 / -1;
  text-align: center;
}
.notificacio {
  color: seagreen;
}
</style>