<template>
    <div :style="style" class="item">
        <div class="itemTitle">{{ title }} ({{ year }})</div>
    </div>
</template>

<script>
export default {
    name: "Item",
    props: {
        item: {
            type: Object,
            required: true,
        }
    },
    data() {
      return {
        poster: this.item.Poster,
        title: this.item.Title,
        year: this.item.Year,
      };
    },
    computed: {
      style() {
        return `backgroundImage: url(${this.poster})`;
      },
    },
};
</script>

<style lang="scss" scoped>

    .item {
        position: relative;
        width: 40vw;
        height: 250px;
        background-color: black;
        background-size: cover;
        background-repeat: no-repeat;
        background-position: center;
        cursor: pointer;
        border: 4px solid white;
        transition: all .3s ease;

        @media (min-width: 768px) {
            width: 25vw;
            height: 280px;
        }

        @media (min-width: 1024px) {
            width: 20vw;
            height: 300px;
        }

        @media (min-width: 1440px) {
            width: 15vw;
            height: 350px;
        }

        @media (min-width: 1920px) {
            height: 420px;
        }

        @media (min-width: 2560px) {
            width: 12vw;
        }
    }

    .item:hover {
        border: 4px solid #64d389;
    }

    .itemTitle {
        position: absolute;
        bottom: 0;
        left: 0;
        height: 25%;
        width: 100%;
        background-color: rgba(0, 0, 0, 0.6);
        color:white;
        display: flex;
        justify-content: center;
        align-items: center;
        text-align: center;
        font-weight: 500;

        @media (min-width: 1920px) {
            height: 15%;
        }
    }

    
</style>