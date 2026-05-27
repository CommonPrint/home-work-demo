<script setup></script>
<template>
  <button class="btn">
    <slot />
  </button>
</template>
<style scoped>
 .btn {
    border: none;
    border-radius: 100px;
    color: white;
    padding: 16px 10px;
    font-size: 24px;
    cursor: pointer;
    background-color: #008BFE;
 }
</style>