<template>
  <div class="heroImage"></div> 
</template>

<script>
export default {
  name: 'HeroImage',
}
</script>


<style lang="scss" scoped>
  .heroImage {
    position: fixed;
    top: 0;
    right: 0;
    background-image: url('../assets/hero-image.jpg');
    background-position: 15% 0%;
    background-size: 1024px;
    width: 100%;
    height: 100vh;
    z-index: -1;

    @media (min-width: 768px) {
      background-size: 1700px;
    }

    @media (min-width: 1024px) {
      background-size: 1900px;
    }

    @media (min-width: 1920px) {
      background-size: 2100px;
    }

    @media (min-width: 2560px) {
      background-size: 2560px;
    }
  }

  .heroImage::after {
    position: absolute;
    top: 0;
    right: 0;
    content: '';
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 1;
  }
</style>
