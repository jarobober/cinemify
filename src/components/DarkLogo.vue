<template>
    <div class="darkLogoWrapper">
        <h1 @click="$emit('backToZero')">Cinemify</h1>
    </div>
</template>

<script>
export default {
    name: 'DarkLogo',
}
</script>

<style lang="scss" scoped>

    .darkLogoWrapper {
        position: absolute;
        top: 30px;

        h1 {
		color: black;
		text-transform: uppercase;
		font-size: 30px;
		font-weight: 600;
		margin-top: 30px;
        cursor: pointer;

            @media (min-width: 768px) {
                font-size: 40px;
                font-weight: 700;
            }
        }
    }


</style>