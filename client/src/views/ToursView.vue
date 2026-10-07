<script setup>
import { ref, onMounted } from 'vue'
import { get } from '../api'

const tours = ref([])
const loading = ref(true)
const error = ref(null)

onMounted(async () => {
  try {
    tours.value = await get('/tours')
  } catch (err) {
    error.value = err.message
  } finally {
    loading.value = false
  }
})
</script>

<template>
  <div>
    <h1>Turer</h1>
    <p v-if="loading">Laddar turer…</p>
    <p v-else-if="error" role="alert">Kunde inte hämta turer: {{ error }}</p>
    <table v-else class="tours">
      <thead>
        <tr>
          <th>Tur</th>
          <th>Av</th>
          <th>Guide</th>
          <th>Längd</th>
          <th>Bilder</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="t in tours" :key="t.id">
          <td>
            <RouterLink :to="`/turer/${t.id}`">{{ t.title }}</RouterLink>
          </td>
          <td>{{ t.user?.display_name }}</td>
          <td>{{ t.guide ? t.guide.title : '-' }}</td>
          <td>{{ Math.round(t.distance_m / 100) / 10 }} km</td>
          <td>{{ t.photos.length }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
.tours {
  width: 100%;
  border-collapse: collapse;
}
.tours th {
  text-align: left;
  padding: 10px;
  font-size: 13px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  color: #4a554f;
  background: #e8e4d8;
}
.tours td {
  padding: 8px 10px;
  border-bottom: 1px solid #eee;
}
</style>
