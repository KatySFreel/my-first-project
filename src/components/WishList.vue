<template>
  <h1>
    Список желаний
  </h1>

  <AppCard 
    v-for="(card, i) in cards"
    :key="card.id"
    :card="card"
    :index="i"
    @click="emit('click-by-card', card)"
  />
</template>

<script setup>
  import AppCard from './AppCard.vue'

  const props = defineProps({
    cards: {
      type: Array
    }
  })

  const emit = defineEmits([
    'click-by-card'
  ])
</script>
