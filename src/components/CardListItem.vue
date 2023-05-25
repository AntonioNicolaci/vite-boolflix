<script>
import LangFlag from 'vue-lang-code-flags';
export default {

    data() {
        return {
            linkPoster: `https://image.tmdb.org/t/p/w500/${this.poster}`,
        }
    },
    props: {
        title: String,
        orTit: String,
        orLang: String,
        vote: Number,
        poster: String,
    },
    methods: {
        posterPlaceholder () {
            this.linkPoster = '../../public/img/poster-placeholder.svg'
        },
    },

    components: {
        LangFlag,
    },
}
</script>

<template>
    <div>
        <img :src="linkPoster" alt="poster" @error="posterPlaceholder">
        <span>
            Titolo: {{ title }}
        </span>
        <span>
            Titolo Originale: {{ orTit }}
        </span>
        <span>
            Lingua Originale: {{ orLang }}
            <lang-flag :iso="orLang" />
        </span>
        <span>
            Voto: {{ Math.floor(vote) }}
        </span>
    </div>
    
</template>

<style lang="scss" scoped>
    div {
        border: 2px solid black;
        color: #fff;
        background-color: rgb(110, 110, 110,);
        display: flex;
        flex-direction: column;
        max-width: calc(100% / 6 - 1em);
    }
    span {
        border-bottom: 2px solid black;
        &:last-child {
            border: none;
        }
    }
    img {
        max-width: 100%;
    }
</style>