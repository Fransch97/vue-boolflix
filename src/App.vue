<template>
  <div id="app">
    <AppHeader />
    <div v-if="loader" class="text-center">
      <div class="lds-ring "><div></div><div></div><div></div><div></div></div>
    </div>
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import axios from "axios";

export default {
    name: "App",
    data() {
        return {
            apiUrl: "https://api.themoviedb.org/3/search/movie",
            apiStructure:{
              api_key: "2a58d3ca96348e8aa76ec66be55ffce4",
              language: "it-IT",
              query:"potter"
            },
            loader: true,
        };
    },
    methods: {
      getApi(){
         this.loader = true
        axios.get(this.apiUrl,{
          params:this.apiStructure
        })
        .then(r=>{
          console.log(r.data.results)
          this.loader = false
        })
        .catch(err=>{
          console.log("LOL!" ,err)
        })
      }
    },
    mounted() {
      this.getApi()
    },
    components: { AppHeader }
}
</script>

<style lang="scss">
@import "./assets/style/global";
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
