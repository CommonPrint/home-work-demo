<script setup lang="ts">
import { ref } from 'vue';

interface Props {
  index?: string | number;
  front: string;
  back: string;
}

withDefaults(defineProps<Props>(), {
  index: '01',
});

const isFlipped = ref(false);

function flipCard() {
  isFlipped.value = !isFlipped.value;
}
</script>

<template>
  <div class="card">
    <div
      class="card__inner"
      :class="{ 'card__inner--flipped': isFlipped }"
    >
      <!-- FRONT -->
      <fieldset class="card__face card__face--front">
        <legend class="card__index">{{ index }}</legend>

        <div class="card__content">
          {{ front }}
        </div>

        <legend
          class="card__action"
          @click="flipCard"
        >
          ПЕРЕВЕРНУТЬ
        </legend>
      </fieldset>

      <!-- BACK -->
      <fieldset class="card__face card__face--back">
        <legend class="card__index">{{ index }}</legend>

        <div class="card__content">
          {{ back }}
        </div>

        <legend
          class="card__action"
          @click="flipCard"
        >
          НАЗАД
        </legend>
      </fieldset>
    </div>
  </div>
</template>

<style scoped>
.card {
  width: 400px;
  height: 600px;
  padding: 24px;
  border-radius: 24px;
  box-shadow:
    0 10px 30px rgba(0, 0, 0, 0.08),
    0 2px 6px rgba(0, 0, 0, 0.04);
  perspective: 1200px;
}

.card__inner {
  position: relative;
  width: 100%;
  height: 100%;
  transition: transform 0.7s ease;
  transform-style: preserve-3d;
}

.card__inner--flipped {
  transform: rotateY(180deg);
}

.card__face {
  position: absolute;
  inset: 0;
  margin: 0;
  padding: 28px;
  border: 2px solid #c4dfff;
  border-radius: 24px;
  backface-visibility: hidden;
  box-shadow:
    0 10px 30px rgba(0, 0, 0, 0.08),
    0 2px 6px rgba(0, 0, 0, 0.04);
}

.card__face--back {
  transform: rotateY(180deg);
}

.card__index {
    position: absolute;
    font-size: 24px;
    top: -14px;
    left: 16px;
    background: #fff;
}

.card__content {
  height: 100%;

  display: flex;
  align-items: center;
  justify-content: center;

  font-size: 32px;
  text-align: center;
}

.card__action {
  margin: 0 auto;
    cursor: pointer;
    font-weight: 700;
    letter-spacing: 0.15em;
    user-select: none;
    position: absolute;
    left: 30%;
    bottom: -12px;
    background: #fff;
}

.card__action:hover {
  opacity: 0.7;
}
</style>