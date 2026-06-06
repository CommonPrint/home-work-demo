<script setup>
import { ref } from 'vue';
import Card from './components/Card.vue';

const cardData = ref([
  {
    word: 'car',
    translation: 'автомобиль',
    state: 'closed',
    status: 'success'
  },
  {
    word: 'window',
    translation: 'стекло',
    state: 'opened',
    status: 'error'
  },  
  {
    word: 'camels',
    translation: 'караван верблюдов',
    state: 'opened',
    status: 'both'
  },
]);
</script>

<template>
  <ul class="row">
    <li v-for="(item, index) in cardData" :key="index">
      <Card :data="item" />
    </li>
  </ul>
</template>

<style scoped>
.row {
  display: flex;
  gap: 20px;
}
</style>
