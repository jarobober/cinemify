<template>
    <div class="outerWrapper">
        <div class="innerWrapper">
            <div class="poster">
                <img :src="poster || 'https://i.pinimg.com/736x/fe/e1/84/fee18481df61ce4220956dc8f44d09e8--black-background-wallpaper-black-backgrounds.jpg'" />
            </div>
            <div class="description">
                <h2 class="title">{{ title }} ({{ year }})</h2>
                <div class="loaderContainer">
                    <div class="loader centered" v-if="beforeData" />
                </div>  
                <table class="info" v-if="!beforeData">
                    <tr><th>Runtime:</th> <td>{{ runtime }}</td></tr>
                    <tr><th>Country:</th> <td>{{ country }}</td></tr>
                    <tr><th>Director:</th> <td>{{ director }}</td></tr>
                    <tr><th>Actors:</th> <td>{{ actors }}</td></tr>
                    <tr><th>Plot:</th> <td>{{ plot }}</td></tr>
                </table>
            </div>
        </div>
        <div class="close" @click="$emit('closeModal')" />
    </div>
</template>

<script>
import axios from 'axios';

const APIID = 'http://www.omdbapi.com/?apikey=becf1f46&i=';

export default {  
    name: 'Modal',
    props: {
        item: {
            type: Object,
            required: true,
        },
    },
    data() {
        return {
            poster: null,
            title: null,
            year: null,
            runtime: null,
            country: null,
            director: null,
            actors: null,
            plot: null,
            movieId: null,
            beforeData: true,
        };
    },
    created() {
        if (this.item.Poster === "N/A") {
            this.poster = "https://makitweb.com/demo/broken_image/images/noimage.png"
        } else {
            this.poster = this.item.Poster;
        }
        this.title = this.item.Title;
        this.year = this.item.Year;
        this.movieId = this.item.imdbID;

        axios.get(`${APIID}${this.movieId}`)
            .then((response) => {
                this.runtime = response.data.Runtime;
                this.country = response.data.Country;
                this.director = response.data.Director;
                this.actors = response.data.Actors;
                this.plot = response.data.Plot;
                this.beforeData = false;
            })
            .catch((error) => {
					console.log(error);
			});
    },
}
</script>

<style lang="scss" scoped>

    .outerWrapper {
        width: 100%;
        height: 100%;
        background-color: rgb(224, 222, 222);
        position: fixed;
        top: 0;
        left: 0;
        overflow-y: auto;
        z-index: 2;

        @media (min-width: 768px) {
			width: 80%;
            height: 80%;
            right: 0;
            bottom: 0;
            margin: auto;
            display: flex;
            align-items: center;
            box-shadow: 0 30px 30px -10px rgba(0, 0, 0, 0.3);
		}

    }

    .innerWrapper {
        width: 80%;
        margin: 0 auto;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: space-evenly;
        
        @media (min-width: 1024px) {
			flex-direction: row;
            justify-content: center;
            max-width: 70%;
		}

        .poster {
            margin-top: 60px;
            height: 100%;

            @media (min-width: 1024px) {
                margin: 0 30px 0 0;
                justify-content: center;
            }
        }

        h2 {
            @media (min-width: 1280px) {
                font-size: 28px;
            }
        }

        .title {
            margin-top: 30px;
            align-self: flex-start;
        }

        .info {
            margin: 20px 0 30px 0;
            height: 100%;

            th, td {
                padding-top: 10px;
                vertical-align: top;
                text-align: left;
            }

            th {
                padding-right: 5px;
            }

            @media (min-width: 1280px) {
                font-size: 20px;
            }
        }
    }

    .close {
        position: absolute;
        width: 30px;
        height: 30px;
        padding: 30px;
        right: 0;
        top: 0;
        cursor: pointer;

            &::before,
            &::after {
            position: absolute;
            top: 30px;
            right: 20px;
            content: '';
            width: 20px;
            height: 2px;
            background: black;
            display: block;
            }

            &::before {
            transform: rotate(45deg);
            }

            &::after {
            transform: rotate(-45deg);
            }
    }

    .loaderContainer {
        text-align: center;
    }

</style>
