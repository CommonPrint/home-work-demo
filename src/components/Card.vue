<script setup lang="ts">
import { ref, inject, Ref } from 'vue';
import SuccessIcon from '../icons/SuccessIcon.vue';
import FailedIcon from '../icons/FailedIcon.vue';

const { data } = defineProps(['data']);

const points = ref(0); // Очки за правильные ответы
const isFlipped = ref(false);
const activeCount = inject<Ref<number>>("activeCount")!;

function flipCard() {
  isFlipped.value = !isFlipped.value;
}

function correctWord(i, boolVal) {
  if (data.isCorrect === boolVal) {
    data.status = 'success'
    points.value++;
  } else {
    data.status = 'error'
  }
  data.state = 'opened';
  activeCount.value++;
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
        <legend class="card__index">
            <div>{{ data.index }}</div>
            <div class="icon-success">
                <SuccessIcon v-if="data.status === 'success'" />
                <FailedIcon v-else-if="data.status === 'error'" />
            </div>
        </legend>

        <div class="card__content">
          {{ data.word }}
        </div>

        <legend
          v-show="!data.status"
          class="card__action"
          @click="flipCard"
        >
          ПЕРЕВЕРНУТЬ
        </legend>
      </fieldset>

      <!-- BACK -->
      <fieldset class="card__face card__face--back">
        <legend v-show="data.state === 'opened'" class="card__index card__index--back">
            <div>{{ data.index }}</div>
            <div class="icon-success">
                <SuccessIcon v-if="data.status === 'success'" />
                <FailedIcon v-else-if="data.status === 'error'" />
            </div>
        </legend>

        <div class="card__content">
          {{ data.translation }}
        </div>

        <legend
          v-show="data.state === 'closed'"
          class="card__action"
          @click="flipCard"
        >
          <div class="both-status">
            <FailedIcon @click="correctWord(data.index, false)" />
            <SuccessIcon @click="correctWord(data.index, true)" />
          </div>
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

.card__index--back {
    display: flex;
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
    display: flex;
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

.icon-success {
    position: absolute;
    left: 160px;
    z-index: 11;
}

.both-status {
    display: flex;
    gap: 20px;
}
</style>