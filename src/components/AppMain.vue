<template>
    <main>
        <div v-for="(film, index) in films" :key="`film-${index}`">
        <p>{{film.title}}</p>
        <p>{{film.original_title}}</p>
        <p>{{film.original_language}}</p>
        <p>{{film.vote_average}}</p>
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

<style>

</style>