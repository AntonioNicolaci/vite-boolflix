<script>
    import CardItem from "./components/CardListItem.vue";
    import axios from 'axios';
    export default {
        data() {
            return {
                FilmJSON: [],
                SeriesJSON: [],
                research: '',
            }
        },

        methods: {
            resAPI (res) {
                const optionsFilm = {
                    method: 'GET',
                    url: 'https://api.themoviedb.org/3/search/movie',
                    params: {query: res, include_adult: 'false', language: 'it-IT', page: '1'},
                    headers: {
                        accept: 'application/json',
                        Authorization: 'Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiIyMWU2NjFkMjdiZWEzNjVkODUwOTY2NDNkMjc2NjBkOSIsInN1YiI6IjY0NmRlNDMyMzNhMzc2MDExZWM1ZWFlNyIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.yVZhwZBeOESjgEA_ZLAxN2yZU7Ky4FABBNEesoLZNQQ'
                    }
                };
                axios
                    .request(optionsFilm)
                    .then(response => {
                        this.FilmJSON = response.data;
                    });
                const optionsSeries = {
                    method: 'GET',
                    url: 'https://api.themoviedb.org/3/search/tv',
                    params: {query: res, include_adult: 'false', language: 'it-IT', page: '1'},
                    headers: {
                        accept: 'application/json',
                        Authorization: 'Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiIyMWU2NjFkMjdiZWEzNjVkODUwOTY2NDNkMjc2NjBkOSIsInN1YiI6IjY0NmRlNDMyMzNhMzc2MDExZWM1ZWFlNyIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.yVZhwZBeOESjgEA_ZLAxN2yZU7Ky4FABBNEesoLZNQQ'
                    }
                };
                axios
                    .request(optionsSeries)
                    .then(response => {
                        this.SeriesJSON = response.data;
                    });
            }
        },

        components: {
            CardItem,
        }
    }
</script>

<template>
    <header>
        <h1>Boolflix</h1>
        <div>
            <input type="text" v-model="research">
            <button @click="resAPI(research)">Cerca</button> 
        </div>
    </header>

    <main>
        <h2>Lista Film</h2>
        <div id="listFilm">
            <CardItem v-for="film in FilmJSON.results"
                :title="film.title"
                :orTit="film.original_title"
                :orLang="film.original_language"
                :vote="film.vote_average"
            />
        </div>
        <h2>Lista Serie TV</h2>
        <div id="listSeries">
            <CardItem v-for="tv in SeriesJSON.results"
                :title="tv.name"
                :orTit="tv.original_name"
                :orLang="tv.original_language"
                :vote="tv.vote_average"
            />
        </div>
    </main>
    
</template>

<style lang="scss" scoped>
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        background-color: #000;
        padding: 1em .4em;

        h1 {
            color: red;
        }

        input[type="text"] {
            border: none;
            height: 2.5em;
            &:focus-visible {
                outline: 1px solid red;
                box-shadow: 0px 0px 20px 1px red;
            }
        }
        
        button {
            border: none;
            height: 2.5em;
            background-color: red;
            color: #fff;
            font-weight: bold;
            padding-inline: .4em;
        }
    
    
    }

    #listFilm, #listSeries {
        display: flex;
        flex-wrap: wrap;
        gap: 1em;
        margin: 2em;
    }
    
</style>
