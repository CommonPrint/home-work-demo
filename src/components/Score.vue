<script setup>
import HeartIcon from '../icons/Heart.vue';
const props = defineProps({
    score: {
        type: Number,
        required: true
    }
});
</script>

<template>
  <button class="btn score">
    <span>{{ score }}</span>
    <HeartIcon />
  </button>
</template>

<style scoped>
.btn {
    border: none;
    cursor: pointer;
}
.score {
    display: flex;
    align-items: center;
    gap: 10px;
    border-radius: 36px;
    color: #008BFE;
    font-size: 16px;
    font-weight: 700;
    padding: 12px 24px;
    background-color: #CCE8FF;
}
</style>