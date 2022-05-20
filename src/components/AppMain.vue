<template>
    <main class="d-flex flex-wrap justify-content-center">
        <div v-for="(film, index) in films" :key="`film-${index}`" class="d-flex">
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

<style lang="scss">
main{
    div{
        background-color: rgb(55, 55, 55);
        height: 300px;
        width: 300px;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        margin: 30px;
        padding: 40px;
    }
}

</style>