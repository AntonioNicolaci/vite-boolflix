<script>

export default {

    data() {
        return {
            linkImg: `http://purecatamphetamine.github.io/country-flag-icons/3x2/${ this.orLang.toUpperCase()}.svg`,
        }
    },
    props: {
        title: String,
        orTit: String,
        orLang: String,
        vote: Number,
    },
    methods: {
        placeHolder () {
            this.linkImg = '../../public/img/International_Flag_of_Planet_Earth.svg'
        }
    }
}
</script>

<template>
    <div>
        <span>
            Titolo: {{ title }}
        </span>
        <span>
            Titolo Originale: {{ orTit }}
        </span>
        <span>
            Lingua Originale: {{ orLang }}
            <img
                :alt="orLang"
                :src="linkImg"
                @error="placeHolder"
                />
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