<template>
  <div class="Appfilmcard container ">
    <h1>{{filmApi.title}}</h1>
    <div class="container d-flex ">
      <img :src="`https://image.tmdb.org/t/p/w500${filmApi.poster_path}`" alt="">
      <div class="info-box d-inline-block mx-4">
        <h2>Titolo originale: {{filmApi.original_title}}</h2>
        
        <p>{{filmApi.overview}}</p>
        <p>Data di rilascio: {{filmApi.release_date.split("-").reverse().join("  ")}}</p>
        <p>Linuga: {{filmApi.original_language}}</p>
        <p>Voto: {{filmApi.vote_average}}</p>

        <button class="btn btn-danger" @click="$emit('back', false)">Torna ai film</button>
      </div>

    </div>
  </div>
</template>

<script>
export default {
name : "AppFilmCard",
props:{
    filmApi: Object
}
}
</script>

<style lang="scss" scoped>
.Appfilmcard{
  position: fixed;
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
</style>