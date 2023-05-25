<script>
import LangFlag from "vue-lang-code-flags";
import { BIconStar, BIconStarFill } from 'bootstrap-icons-vue'
export default {
    data() {
        return {
            linkPoster: `https://image.tmdb.org/t/p/w500/${this.poster}`,
            starAverage: Math.floor(this.vote / 2),
        };
    },
    props: {
        title: String,
        orTit: String,
        orLang: String,
        vote: Number,
        poster: String,
        des: String,
    },
    methods: {
        posterPlaceholder() {
            this.linkPoster = "../../public/img/poster-placeholder.svg";
        },
    },

    components: {
        LangFlag,
        BIconStar,
        BIconStarFill,
    },
};
</script>

<template>
    <div class="card">
        <div class="card-inner">
            <div class="card-front">
                <img :src="linkPoster" alt="poster" @error="posterPlaceholder" />
            </div>
            <div class="card-back">
                <span> Titolo: {{ title }} </span>
                <span> Titolo Originale: {{ orTit }} </span>
                <span>
                    Lingua Originale:
                    <lang-flag :iso="orLang" />
                </span>
                <span>
                    {{ des }}
                </span>
                <div id="divStar">
                    <template v-for="n in 5">
                        <BIconStarFill v-if="starAverage > n" />
                        <BIconStar v-else />
                    </template>
                </div>
            </div>

        </div>

    </div>
</template>

<style lang="scss" scoped>
.card {
    width: calc(100% / 6 - 1em);
    height: 446px;
    background-color: transparent;
    perspective: 1000px;
}

.card-inner {
    position: relative;
    width: 100%;
    height: 100%;
    text-align: center;
    transition: transform 0.8s;
    transform-style: preserve-3d;
    border: 2px solid rgb(200, 200, 200);
}

.card:hover .card-inner {
    transform: rotateY(180deg);
}

.card-front,
.card-back {
    position: absolute;
    width: 100%;
    height: 100%;
    backface-visibility: hidden;
}

.card-front {
    background-color: rgb(87, 100, 114);
}

.card-back {
    background-color: #000;
    color: white;
    transform: rotateY(180deg);
    display: flex;
    flex-direction: column;
}

img {
    max-width: 100%;
    height: 442px;
}

#divStar {
    display: flex;
    color: rgb(255, 255, 0);
    align-self: center;
}
</style>
