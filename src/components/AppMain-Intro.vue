<template>
  <div class="container">
    <h1 class="pop">I più popolari del momento</h1>
    <div v-for="(gen, index) in FilmGen" :key="`gen-${index}`" >
      <div v-if="gen.film.length > 1">
        
        <h1>{{gen.name}}</h1>
        <div class="films d-flex ">
          <div v-for="(fil, index) in gen.film" :key="`film${index}`" class="card-sc">
            <div>
              <img :src="`https://image.tmdb.org/t/p/w500${fil.poster_path}`" alt="">
              <p>Titolo: {{fil.title}}</p>
               <p>Titolo originale: {{fil.original_title}}</p>
              <p>Lingua: {{fil.original_language}}</p>
              <p>Voto: {{fil.vote_average}}</p>
            </div>
          </div>
      </div>
      </div>
    </div>
  </div>

  
</template>

<script>
export default {
    name: "AppMain-Intro",
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
    }

}
</script>

<style lang="scss">
.pop{
  font-weight: bold;
  font-size: 4rem;
  padding: 30px 0;
}

.films{
  overflow: auto;
}
.card-sc{
  div{
        background-color: rgb(55, 55, 55);
        height: 40vh;
        width: 28vh;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        margin: 30px;
        overflow: hidden;
        img{
          width: 100%;
        }
    }
}
</style>