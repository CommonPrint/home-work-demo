<script setup>
import Score from './Score.vue';
</script>

<template>
    <header class="header">
        <nav class="row">
            <a class="link" href="#">ЗАПОМНИ СЛОВО</a>
            <Score :score="100" />
        </nav>
    </header>
</template>

<style scoped>
.header {
    margin: 36px 62px;
}
.link {
    font-size: 16px;
    font-weight: 700;
    text-decoration: none;
    color: #000;
}
.row {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
</style>
