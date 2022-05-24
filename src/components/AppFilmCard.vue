<template>
  <div class="Appfilmcard container ">
    <h1>{{filmApi.title}}</h1>
    <div class="container d-flex ">
      <img :src="`https://image.tmdb.org/t/p/w500${filmApi.poster_path}`" alt="">
      <div class="info-box d-inline-block mx-4">
        <h2 v-if="filmApi.original_title">Titolo originale: {{filmApi.original_title}}</h2>
        <h2 v-else>Titolo originale: {{filmApi.original_name}}</h2>
        
        <p>{{filmApi.overview}}</p>
        <p v-if="filmApi.release_date">Data di rilascio: {{filmApi.release_date.split("-").reverse().join(".")}}</p>
        <p v-else>Data di rilascio: {{filmApi.first_air_date.split("-").reverse().join(".")}}</p>
        <p>Attori: <span v-for="(actor,index) in attori" :key="`attore-${index}`">{{actor}}, </span> </p>
        <p v-for="(genre, index) in filmgenre" :key="`genre-${index}`">Genere {{index + 1}}: {{genre.name}}</p>
       
        <lang-flag 
        v-if="oklng.includes(filmApi.original_language)" 
        :iso="filmApi.original_language"  class="flagi"/>
        <p v-else>lingua: {{filmApi.original_language}}</p>
        <star-rating
                class="stars"
                :increment="0.01"
                :rating="filmApi.vote_average/2"
                :star-size="27"
                :read-only="true"
                ></star-rating>

        <button class="btn btn-danger" @click="$emit('back', false)">Torna ai film</button>
      </div>

    </div>
  </div>
</template>

<script>
import LangFlag from 'vue-lang-code-flags';
import StarRating from 'vue-star-rating';
import axios from 'axios';

export default {
name : "AppFilmCard",
components: {
        LangFlag,
        StarRating

    },

props:{
    filmApi: Object
},
data() {
      return {
              api_key: "2a58d3ca96348e8aa76ec66be55ffce4",
              oklng : ["ar","am","az","be","bn","bg","zh","ca","cs","en","et","fr","de","el","ha","hi","hu","it","ja","jv","km","ko","lv","ms","mr","fa","pl","pt","ro","ru","es","sw","ta","te","th","tr","uz","vi",],
              crew: [],
              attori: [],
              filmgenre: []
      }
    },
mounted() {
  axios.get('https://api.themoviedb.org/3/movie/' + this.filmApi.id + '/credits?api_key=' + this.api_key + '&language=en-US')
  .then((r)=>{
    this.crew = r.data.crew
    for(let i = 0; i < 5 ; i++){
      this.attori.push(this.crew[i].name)
    }
    })
  axios.get('https://api.themoviedb.org/3/movie/' + this.filmApi.id + '?api_key=' + this.api_key + '&language=en-US')
  .then((r)=>{
    this.filmgenre = r.data.genres
  
    })
},
}
</script>

<style lang="scss" scoped>
.vue-star-rating{
    display: flex;
  align-items: center;
  flex-direction: row;
  margin: 20px 0;
}
.Appfilmcard{
  overflow-y: auto;
  position: fixed;
  height: 70vh;
  top: 15%;
  background-color: black;
  left: 50%;
  transform: translateX(-50%);
  width: 80vw;
  padding: 50px;
}
h1{
  font-weight: bold;
  text-align: center;
  padding-bottom: 40px;
}
.info-box{
  display: flex;
  
}
img{
    height:42vh;
        width: 28vh;
  }
  .flagi{
    width: 50px;
    height: 50px;
  }
</style>