<template>
    <div class="page">
        <Header class="page__header"></Header>
        <main class="page__main main">
            <nuxt></nuxt>
        </main>
        <Footer class="page__footer"></Footer>
    </div>
</template>

<script setup>
import Header from "../components/Header";
</script>

<style lang="scss">
.page {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
}

.main {
    display: flex;
    flex-grow: 1;
}
</style>
