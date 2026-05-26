<script setup>
const currentDate = new Date();
</script>

<template>
  <div class="app">
    <h1>Current Date and Time</h1>
    <p>{{ currentDate.toLocaleString() }}</p>
  </div>
</template>
