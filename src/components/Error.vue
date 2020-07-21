<template>
    <p class="errorText">Unfortunately there's no matching title. Try another.</p>
</template>

<script>
export default {
    name: 'Error',
}
</script>

<style lang="scss" scoped>
    .errorText {
        max-width: 90%;
        margin: 50px 10px;
        border: 1px solid black;
        padding: 5px;
        color:rgb(238, 128, 128);
    }
</style>