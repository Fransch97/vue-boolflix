<template>
  <div id="app">
    <div v-if="page">
      <AppHeader @search_key="sk"/>
      <div v-if="loader" class="text-center">
        <div class="lds-ring "><div></div><div></div><div></div><div></div></div>
      </div>
      <AppMain v-else :films="films"/>
    </div>
    <div id="logo" v-else>
      <img src="./assets/img/logo.png" alt="">
    </div>
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import axios from "axios";
import AppMain from "./components/AppMain.vue";

export default {
  name: "App",
  components: { AppHeader, AppMain },
    data() {
        return {
            apiUrl: "https://api.themoviedb.org/3/search/movie",
            apiStructure:{
              api_key: "2a58d3ca96348e8aa76ec66be55ffce4",
              language: "it-IT",
              query:"potter"
            },
            loader: true,
            films:[],
            page: false
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
        this.apiStructure.query =  sk
        this.getApi()
      },
      
    },
    mounted() {
      const open = new Audio(require('./assets/sound/Netflix-Intro-Sound-Effect.mp3'))
      open.play()
      setTimeout(()=>{
        this.page = true
        this.getApi()
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
