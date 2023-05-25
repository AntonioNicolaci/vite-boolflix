<script>
export default {
    props: {
        title: String,
        orTit: String,
        orLang: String,
        vote: Number,
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
</style>