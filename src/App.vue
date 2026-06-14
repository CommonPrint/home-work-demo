<script setup>
import { provide, onMounted, ref } from 'vue';
import Card from './components/Card.vue';

const cardData = ref([]);
const activeCount = ref(0);
const countLength = ref(0);

provide("activeCount", activeCount);

async function getData() {
  const res = await fetch(`http://localhost:8080/api/random-words`)
  if(res.status != 200) {
    return;
  }
  return await res.json();
}

function loadData() {
  getData().then((data) => {
    cardData.value = data;
    cardData.value.map((item, index) => {
      if (index === 2 || index === 5) {
        item.isCorrect = false;
      } else {
        item.isCorrect = true;
      }
      item.index = index;
      item.state = 'closed';
    });
    countLength.value = cardData.value.length;
  });
}

onMounted(() => {
  loadData();
});

const restart = () => {
  activeCount.value = 0;
  loadData();
}
</script>

<template>
  <ul class="row">
    <li v-for="(item, index) in cardData" :key="index">
      <Card :data="item" />
    </li>
  </ul>
  <button 
    class="btn"
    :disabled="activeCount !== countLength" 
    @click="restart"
  >Начать заново</button>
</template>

<style scoped>
.row {
  display: flex;
  gap: 20px;
  flex-wrap: wrap;
  justify-content: center;
}

.btn {
  width: fit-content;
  align-self: center;
  color: #fff;
  background: #008BFE;
  border-radius: 25px;
  padding: 16px 30px;
  font-size: 20px;
  margin-bottom: 40px;
}

.btn:disabled {
  cursor: disabled;
  background: gray;
  color: #000;
}
</style>
