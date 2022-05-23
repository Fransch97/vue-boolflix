<template>
    <main class="d-flex flex-wrap justify-content-center">
        <div v-for="(film, index) in films" :key="`film-${index}`" class="card-sc ">
            <img :src="`https://image.tmdb.org/t/p/w500${film.poster_path}`" alt="">
            <div class="card-info">
                <p v-if="film.title">Titolo: {{film.title}}</p>
                <p v-else>Titolo: {{film.name}}</p>
                <p v-if="film.original_title">Titolo originale: {{film.original_title}}</p>
                <p v-else>Titolo originale: {{film.original_name}}</p>
                <lang-flag 
                v-if="oklng.includes(film.original_language)" 
                :iso="film.original_language"  class="flagi"/>
                <p v-else>lingua: {{film.original_language}}</p>
                <p>Voto: {{film.vote_average}}</p>
                <star-rating
                class="stars"
                :increment="0.01"
                :rating="film.vote_average/2"
                :star-size="27"
                :read-only="true"
                ></star-rating>
                <br>
                <button class="btn btn-danger" @click="$emit('filmID', film)">Film</button>
            </div>
        </div>
    </main>
</template>

<script>
import LangFlag from 'vue-lang-code-flags';
import StarRating from 'vue-star-rating';

export default {
    name: "AppMain",
    components: {
        LangFlag,
        StarRating

    },
    props:{
        films: Array
    },
    data() {
      return {
        oklng : ["ar","am","az","be","bn","bg","zh","ca","cs","en","et","fr","de","el","ha","hi","hu","it","ja","jv","km","ko","lv","ms","mr","fa","pl","pt","ro","ru","es","sw","ta","te","th","tr","uz","vi",]
      }
    },

}
</script>

<style lang="scss" scoped>
.card-sc{
       
        background-color: rgb(55, 55, 55);
        height: 42vh;
        width: 28vh;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        margin: 30px;
        overflow: hidden;
        position: relative;
        img{
          width: 100%;
        }
         .card-info{
          overflow-y: auto;
          overflow-x: hidden;
          position: absolute;
          top: 0;
          left:0;
          margin: 0;
          width: 100%;
          height: 100%;
          background-color: rgba(0, 0, 0, 0.641);
          padding: 20px;
          text-align: center;
          display: none;
        }
         &:hover .card-info{
            display: block;
          }
}
.flagi{
    width: 50px;
    height: 50px;
  }

</style>