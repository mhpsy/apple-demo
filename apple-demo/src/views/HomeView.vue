<script setup>

</script>

<template>
    <div class="home-page">
        <div v-for="i in 19">{{ i }}</div>
    </div>
</template>
<style scoped>
.home-page {
    border: 1px red solid;
    display: grid;
    grid-template-rows: repeat(3,100px);
    grid-template-columns: repeat(3,100px);

    & > div {
        border: 1px dodgerblue solid;
    }
}

</style>
