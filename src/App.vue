<template>
  <div id="app" @mousemove="afk()">
    <!--AFTER INTRO  -->
    <div v-if="page">

      <!-- HEADER  -->
      <AppHeader @search_key="sk" @search_lib="setlib"/>
      <!--END HEADER  -->
      <div v-if="afker">
        <AppAfkJabo :films="introMain.films" :searchfilms="films" />
      </div>
      
      <!-- LOADER  -->
      <div v-if="loader" class="text-center">
        <div class="lds-ring "><div></div><div></div><div></div><div></div></div>
      </div>
      <!--END LOADER  -->
      <!-- MAIN  -->
      <div v-else class="realmain">
        <AppMainIntro v-if="apiStructure.query === ''" :films="introMain.films" :genre="introMain.genres" @filmID="sendcard"/>
        <AppMain v-else :films="films"  @filmID="sendcard"/>
        <AppFilmCard v-if="appCard" :filmApi="cardID" @back="back"/>
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
import AppAfkJabo from "./components/AppAfkJabo.vue";

export default {
  name: "App",
  components: { AppHeader, AppMain, AppMainIntro, AppFilmCard, AppAfkJabo },
    data() {
        return {
            searchlibrary: "",
            apiUrl: "https://api.themoviedb.org/3/search/",
            apiStructure:{
              api_key: "2a58d3ca96348e8aa76ec66be55ffce4",
              language: "it-IT",
              query:""
            },
            loader: true,
            films:[],
            introMain:{
              apiUrl:"https://api.themoviedb.org/3/trending/all/day",
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
            appCard: false,
            afker: false,
            banner: null,
        };
    },
    computed:{

    },
    methods: {
      setlib(key){
        this.searchlibrary = key
        if(this.apiStructure.query !== ""){
          if(this.searchlibrary === "all"){ this.searchlibrary = "multi"}
          this.getApi()
        }else{
          if(key === "all"){
           this.introMain.apiUrl =  "https://api.themoviedb.org/3/trending/all/day"
          } else if(key === "movie"){
           this.introMain.apiUrl =  "https://api.themoviedb.org/3/trending/movie/day"
          }else{
           this.introMain.apiUrl =  "https://api.themoviedb.org/3/trending/tv/day"
          }
           this.introMainFunction()
        }
      },
      getApi(){
         this.loader = true
          axios.get(this.apiUrl + this.searchlibrary,{
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
        if (!(sk === "")){
            this.apiStructure.query =  sk
          // if(this.searchlibrary === "all"){ this.searchlibrary = "multi"}
            this.getApi()
          }else{
          this.introMainFunction()
            this.apiStructure.query =  sk
          this.loader = false
          } 
      },
      introMainFunction(){
        this.loader= true
        this.introMain.getGenre.page = 1
        this.introMain.genres = []
        this.introMain.films =[]
        axios.get("https://api.themoviedb.org/3/genre/movie/list?api_key=2a58d3ca96348e8aa76ec66be55ffce4&language=it-IT")
        .then(r=>{
          console.log(r.data.genres)
          this.introMain.genres = r.data.genres
        })
        .catch(e=>{
          console.log(e)
          this.loader = false
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
                if(i == this.introMain.times - 1 ){
                  this.loader = false
                }
              });
            
              console.log(this.introMain.films)
            })
            
          }

         
      },
      sendcard(obj){
        this.cardID = obj
        this.appCard = true
      },
      back(bool){
        this.appCard = bool
      },
      afk(){
        clearInterval(this.banner)
        this.afker = false

        this.banner = setTimeout(() => {
          this.afker = true
        }, 3000);
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
.realmain{
  position: relative;
}

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
