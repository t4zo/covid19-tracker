<template>
  <div class="grid md:grid-cols-2 gap-4">
    <!-- Box 1 -->
    <div class="shadow-md bg-blue-100 p-10 text-center rounded">
      <h3 class="text-3xl text-blue-900 font-bold mb-4">Casos Confirmados</h3>
      <div class="text-2xl mb-4">
        <span class="font-bold">Novos:</span>
        {{ stats.NewConfirmed.toLocaleString() }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">Total:</span>
        {{ stats.TotalConfirmed.toLocaleString() }}
      </div>
    </div>
    <!-- Box 2 -->
    <div class="shadow-md bg-blue-100 p-10 text-center rounded">
      <h3 class="text-3xl text-blue-900 font-bold mb-4">Mortes Confirmadas</h3>
      <div class="text-2xl mb-4">
        <span class="font-bold">Novos:</span>
        {{ stats.NewDeaths.toLocaleString() }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">Total:</span>
        {{ stats.TotalDeaths.toLocaleString() }}
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'Boxes',
  props: {
    stats: {}
  }
})
</script>