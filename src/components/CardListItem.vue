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
    <img :src="linkPoster" alt="poster" @error="posterPlaceholder" />
    <span> Titolo: {{ title }} </span>
    <span> Titolo Originale: {{ orTit }} </span>
    <span>
      Lingua Originale: {{ orLang }}
      <lang-flag :iso="orLang" />
    </span>
    <div id="divStar"> 
        <template v-for="n in 5">
            <!-- <i :class="['bi', starAverage > n ? 'bi-star-fill' : 'bi-star']"></i> -->
            <BIconStarFill v-if="starAverage > n"/>
            <BIconStar v-else/>
        </template>    
    </div>
  </div>
</template>

<style lang="scss" scoped>
.card {
  border: 2px solid black;
  color: #fff;
  background-color: rgb(110, 110, 110);
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
#divStar {
    display: flex;
}
</style>
