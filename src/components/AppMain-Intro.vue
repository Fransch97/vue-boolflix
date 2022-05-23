<template>
  <div class="container">
    <h1 class="pop">I più popolari del momento</h1>
    <div v-for="(gen, index) in FilmGen" :key="`gen-${index}`" >
      <div v-if="gen.film.length > 1">
        
        <h1>{{gen.name}}</h1>
        <div class="films d-flex ">
          <div v-for="(fil, index) in gen.film" :key="`film${index}`" class="card-sc">
            <div class="position-relative cc">
              <img :src="`https://image.tmdb.org/t/p/w500${fil.poster_path}`" alt="">
              <div class="card-info">
                <p v-if="fil.title">Titolo: {{fil.title}}</p>
                <p v-else>Titolo: {{fil.name}}</p>
                <p v-if="fil.original_title">Titolo originale: {{fil.original_title}}</p>
                <p v-else>Titolo originale: {{fil.original_name}}</p>
                <lang-flag v-if="oklng.includes(fil.original_language)" :iso="fil.original_language"  class="flagi"/>
                <p v-else>lingua: {{fil.original_language}}</p>

                <star-rating
                class="stars"
                :increment="0.01"
                :rating="fil.vote_average/2"
                :star-size="27"
                :read-only="true"
                ></star-rating>



                <button class="btn btn-danger" @click="$emit('filmID', fil)">Film</button>
              </div>
            </div>
          </div>
      </div>
      </div>
    </div>
  </div>

  
</template>

<script>
import LangFlag from 'vue-lang-code-flags';
import StarRating from 'vue-star-rating';
export default {
    name: "AppMain-Intro",
    components: {
        LangFlag,
        StarRating
    },
    data() {
      return {
        oklng : ["ar","am","az","be","bn","bg","zh","ca","cs","en","et","fr","de","el","ha","hi","hu","it","ja","jv","km","ko","lv","ms","mr","fa","pl","pt","ro","ru","es","sw","ta","te","th","tr","uz","vi",]
      }
    },
    props: {
      films:Array,
      genre:Array
    },
    computed:{
      FilmGen(){
        this.genre.forEach((el)=>{
          console.log(el.id, "its working")
          el.film = []
          for(let i = 0; i< this.films.length; i++){
            if(this.films[i].genre_ids[0] == el.id){
              el.film.push(this.films[i]) 
            }
          }
          
        })
          return this.genre



      }
    },
    

}
</script>

<style lang="scss">
.vue-star-rating{
    display: flex;
  align-items: center;
  flex-direction: row;
  margin: 20px 0;
}
.pop{
  font-weight: bold;
  font-size: 4rem;
  padding: 30px 0;
}


.films{
  overflow: auto;
}
.card-sc{
  .cc{
    height: 42vh;
        width: 28vh;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        margin: 30px;
        cursor: pointer;
        overflow: hidden;
        .card-info{
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
        img{
          width: 100%;
        }
    }
     .flagi{
    width: 50px;
    height: 50px;
  }
}
</style>