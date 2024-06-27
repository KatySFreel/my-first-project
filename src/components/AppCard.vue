<template>
  <div class="card">
    <h3 class="card__title">
      {{ card.title }}
    </h3>

    <p class="card__description">
      {{ card.description }}
    </p>

    <div class="card__completed">
      <span
        :class="
        { 'card__completed--yes': card.completed,
          'card__completed--no' : !card.completed
        }"
      >
        {{ card.completed ? 'Исполнено' : 'Не исполнено' }}
      </span>
    </div>
  </div>
</template>

<script setup>
  const props = defineProps({
    index: {
      type: Number
    },
    card: {
      type: Object
    }
  })
</script>


<style scoped>
  .card {
    width: 300px;
    padding: 24px 24px 16px;
    background-color: rgb(241, 248, 255);
    border-radius: 16px;
    margin-bottom: 16px;
	  cursor: pointer;
  }

  .card__title {
    font-size: 18px;
    font-weight: 600;
    margin-bottom: 8px;
  }

  .card__description {
    color: rgb(106, 109, 114);
    margin-bottom: 16px;
  }

  .card__completed {
    display: flex;
    align-items: center;
    gap: 4px;
  }

  .card__completed--yes {
    padding: 0 6px;
    border: 1px solid rgb(42, 182, 231);
    color: rgb(42, 182, 231);
    border-radius: 4px;
  }

  .card__completed--no {
    padding: 0 6px;
    border: 1px solid rgb(166, 182, 197);
    color: rgb(166, 182, 197);
    border-radius: 4px;
  }
</style>
