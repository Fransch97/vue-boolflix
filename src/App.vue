<template>
  <div id="app">
    <!--AFTER INTRO  -->
    <div v-if="page">

      <!-- HEADER  -->
      <AppHeader @search_key="sk"/>
      <!--END HEADER  -->
      
      <!-- LOADER  -->
      <!-- <div v-if="loader" class="text-center">
        <div class="lds-ring "><div></div><div></div><div></div><div></div></div>
      </div> -->
      <!--END LOADER  -->

      <!-- MAIN  -->
      <div >
        <AppMainIntro v-if="apiStructure.query === '' && !appCard" :films="introMain.films" :genre="introMain.genres" @filmID="sendcard"/>
        <AppFilmCard v-else-if="appCard" :filmApi="cardID" @back="back"/>
        <AppMain v-else :films="films"/>
      </div>
      <!--END MAIN  -->

    </div>
    <!--END AFTER INTRO  -->
    
    <!-- INTRO  -->
    <div id="logo" v-else>
      <img src="./assets/img/logo.png" alt="">
    </div>
    <!--END INTRO  -->
  
  
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import axios from "axios";
import AppMain from "./components/AppMain.vue";
import AppMainIntro from "./components/AppMain-Intro.vue";
import AppFilmCard from "./components/AppFilmCard.vue";

export default {
  name: "App",
  components: { AppHeader, AppMain, AppMainIntro, AppFilmCard },
    data() {
        return {
            apiUrl: "https://api.themoviedb.org/3/search/movie",
            apiStructure:{
              api_key: "2a58d3ca96348e8aa76ec66be55ffce4",
              language: "it-IT",
              query:""
            },
            loader: true,
            films:[],
            introMain:{
              apiUrl:"https://api.themoviedb.org/3/trending/movie/day",
              getGenre:{
                api_key: "2a58d3ca96348e8aa76ec66be55ffce4",
                language: "it-IT",
                page: 1,
              },
              times: 10,
              genres: [],
              films:[],
              cardID:{}
            },
            page: false,
            appCard: false
        };
    },
    computed:{

    },
    methods: {
      getApi(){
         this.loader = true
        axios.get(this.apiUrl,{
          params:this.apiStructure
        })
        .then(r=>{
          console.log(r.data.results)
          this.films = r.data.results
          this.loader = false
        })
        .catch(err=>{
          console.log("LOL!" ,err)
        })
      },
      sk(sk){
        console.log(sk)
        if(sk.trim === ""){
          this.introMainFunction()
          this.apiStructure.query =  sk
        }else{
          this.apiStructure.query =  sk
          this.getApi()
        }
      },
      introMainFunction(){
        this.loader = true
        axios.get("https://api.themoviedb.org/3/genre/movie/list?api_key=2a58d3ca96348e8aa76ec66be55ffce4&language=it-IT")
        .then(r=>{
          console.log(r.data.genres)
          this.introMain.genres = r.data.genres
            
        })
          for(let i = 0; i< this.introMain.times; i++){
            this.introMain.getGenre.page++
            axios.get(this.introMain.apiUrl, {
              params: this.introMain.getGenre
            })
            .then(re=>{
              console.log(re.data.results , "sono", i)
              re.data.results.forEach(element => {
                this.introMain.films.push(element)
              });
              
              console.log(this.introMain.films)
            })

          }
          this.loader = false

         
      },
      sendcard(obj){
        this.cardID = obj
        this.appCard = true
      },
      back(bool){
        this.appCard = bool
      }
      
    },
    mounted() {
      const open = new Audio(require('./assets/sound/Netflix-Intro-Sound-Effect.mp3'))
      open.play()
      setTimeout(()=>{
        this.page = true
        this.introMainFunction()
      }, 3000)
      
    }
    
}
</script>

<style lang="scss">
@import "./assets/style/global";

#logo{
  display: flex;
  justify-content: center ;
  align-items: center;
  height: 100vh;
}


.lds-ring {
  display: inline-block;
  position: relative;
  width: 80px;
  height: 80px;
}
.lds-ring div {
  box-sizing: border-box;
  display: block;
  position: absolute;
  width: 64px;
  height: 64px;
  margin: 8px;
  border: 8px solid #a00f0f;
  border-radius: 50%;
  animation: lds-ring 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
  border-color: #a00f0f transparent transparent transparent;
}
.lds-ring div:nth-child(1) {
  animation-delay: -0.45s;
}
.lds-ring div:nth-child(2) {
  animation-delay: -0.3s;
}
.lds-ring div:nth-child(3) {
  animation-delay: -0.15s;
}
@keyframes lds-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
