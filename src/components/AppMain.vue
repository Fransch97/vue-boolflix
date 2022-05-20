<template>
    <main class="d-flex flex-wrap justify-content-center">
        <div v-for="(film, index) in films" :key="`film-${index}`" class="card-sc">
        <img :src="`https://image.tmdb.org/t/p/w500${film.poster_path}`" alt="">
        <p>Titolo: {{film.title}}</p>
        <p>Titolo originale: {{film.original_title}}</p>
        <p>Lingua: {{film.original_language}}</p>
        <p>Voto: {{film.vote_average}}</p>
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

</style>