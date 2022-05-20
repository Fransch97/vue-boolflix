<template>
    <main class="d-flex flex-wrap justify-content-center">
        <div v-for="(film, index) in films" :key="`film-${index}`" class="card-sc ">
            <img :src="`https://image.tmdb.org/t/p/w500${film.poster_path}`" alt="">
            <div class="card-info">
                <p>Titolo: {{film.title}}</p>
                <p>Titolo originale: {{film.original_title}}</p>
                <p>Lingua: {{film.original_language}}</p>
                <p>Voto: {{film.vote_average}}</p>
                <button class="btn btn-danger" @click="$emit('filmID', film)">Film</button>
            </div>
        </div>
    </main>
</template>

<script>
export default {
    name: "AppMain",
    props:{
        films: Array
    }

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

</style>