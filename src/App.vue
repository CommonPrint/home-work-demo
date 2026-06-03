<script setup>
import { ref } from 'vue';
import Card from './components/Card.vue';

const cardData = ref({
  word: 'car',
  translation: 'автомобиль',
  state: 'closed',
  status: 'success'
});
</script>

<template>
  <Card :data="cardData" />
</template>
