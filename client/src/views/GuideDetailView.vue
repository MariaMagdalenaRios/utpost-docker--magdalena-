<script setup lang="ts">
import { ref, watch, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import type { Guide } from '@utpost/shared'
import { get } from '../api'

const route = useRoute()
const guide = ref<Guide | null>(null)
const error = ref<string | null>(null)

const load = async (slug: string) => {
  guide.value = null
  error.value = null
  try {
    guide.value = await get<Guide>(`/guides/${slug}`)
  } catch (err) {
    error.value = (err as Error).message
  }
}

onMounted(() => load(route.params.slug as string))
watch(
  () => route.params.slug,
  (slug) => slug && load(slug as string),
)
</script>

<template>
  <p v-if="error" role="alert">{{ error }}</p>
  <p v-else-if="!guide">Laddar…</p>
  <article v-else>
    <h1>{{ guide.title }}</h1>
    <p class="muted">{{ guide.region }} · {{ guide.difficulty }} · {{ guide.length_km }} km</p>
  </article>
</template>
