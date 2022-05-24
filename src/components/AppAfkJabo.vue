<template>
  <div class="afkJambo">
    <img class="jambo-img" :src="`https://image.tmdb.org/t/p/original${img}`" alt="">
    <img src="../assets/img/logo.png" alt="" id="logo">
</div>
</template>

<script>
export default {
props:{
    films: Array,
    searchfilms: Array
},
data() {
    return {
        filmsbool : null,
        searchfilmsbool : null,
        img: "",
        imgIndex : 0
    }
},
mounted() {
    if(this.films.length > 0){
       setInterval(()=>{
            this.img = this.films[this.imgIndex].backdrop_path
            this.imgIndex++
        },5000)
    }
},
}
</script>

<style lang="scss" >
.afkJambo{
    background-color: black;
    height: 100vh;
    width: 100%;
    position: fixed;
    top: 0;
    z-index: 1000;
    .jambo-img{
        width: 100%;
        animation: mymove 15s infinite;
        transition-delay: all 1s;
    }
    @keyframes mymove {
    0%   {scale: 1.0;}
    25%  {scale: 1.3;}
    50%  {scale: 1.6;}
    75%  {scale: 1.3;}
    100% {scale: 1.0;}
}
    #logo{
        position: fixed;
        bottom: 5%;
        left: 5%;
        z-index: 100;
        width: 600px;
        height: 200px;

    }
}

</style>