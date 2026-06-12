<script setup>
import { onMounted, ref } from 'vue';
import Card from './components/Card.vue';

const cardData = ref([]);

async function getData() {
  const res = await fetch(`http://localhost:8080/api/random-words`)
  if(res.status != 200) {
    return;
  }
  return await res.json();
}

onMounted(() => {
  getData().then((data) => {
    cardData.value = data;
  });
});
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
  flex-wrap: wrap;
}
</style>
