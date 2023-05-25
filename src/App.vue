<script>
import CardItem from "./components/CardListItem.vue";
import axios from "axios";
export default {
  data() {
    return {
      FilmJSON: [],
      SeriesJSON: [],
      research: "",
    };
  },

  methods: {
        resAPI(res, arrType, arrOBJ) {
            arrType.forEach((element, index) => {
                arrOBJ = [];
                const options = {
                    method: "GET",
                    url: `https://api.themoviedb.org/3/search/${element}`,
                    params: {
                        query: res,
                        include_adult: "false",
                        language: "it-IT",
                        page: "1",
                    },
                    headers: {
                        accept: "application/json",
                        Authorization:
                            "Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiIyMWU2NjFkMjdiZWEzNjVkODUwOTY2NDNkMjc2NjBkOSIsInN1YiI6IjY0NmRlNDMyMzNhMzc2MDExZWM1ZWFlNyIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.yVZhwZBeOESjgEA_ZLAxN2yZU7Ky4FABBNEesoLZNQQ",
                    },
                }
                if  (arrType[index] === 'movie'){
                    axios.request(options).then((response) => {
                        return this.FilmJSON = response.data;
                    }) 
                }
                else {
                    axios.request(options).then((response) => {
                        return this.SeriesJSON = response.data;
                    })
                }
            })
        }
},

  components: {
    CardItem,
  },
};
</script>

<template>
  <header>
    <!-- <h1>Boolflix</h1> -->
    <img
      src="https://image.tmdb.org/t/p/w200/wwemzKWzjKYJFfCeiB57q3r4Bcm.png"
      alt="logo"
    />
    <div>
      <input type="text" v-model="research" />
      <button @click="resAPI(research, ['movie', 'tv'])">Cerca</button>
    </div>
  </header>

  <main>
    <h2>Lista Film</h2>
    <div id="listFilm">
      <CardItem
        v-for="film in FilmJSON.results"
        :title="film.title"
        :orTit="film.original_title"
        :orLang="film.original_language"
        :vote="film.vote_average"
        :poster="film.poster_path"
      />
    </div>
    <h2>Lista Serie TV</h2>
    <div id="listSeries">
      <CardItem
        v-for="tv in SeriesJSON.results"
        :title="tv.name"
        :orTit="tv.original_name"
        :orLang="tv.original_language"
        :vote="tv.vote_average"
        :poster="tv.poster_path"
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
  padding: 1em 0.4em;

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
    padding-inline: 0.4em;
  }
}

#listFilm,
#listSeries {
  display: flex;
  flex-wrap: wrap;
  gap: 1em;
  margin: 2em;
}
</style>
