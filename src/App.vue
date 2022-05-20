<template>
  <div id="app">
    <AppHeader />
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import axios from "axios";

export default {
    name: "App",
    data() {
        return {
            apiUrl: "https://api.themoviedb.org/3/",
            apiStructure:{
              api_key: "2a58d3ca96348e8aa76ec66be55ffce4"
            }
        };
    },
    methods: {
      getApi(){
        axios.get(this.apiUrl,{
          params:this.apiStructure
        })
        .then(r=>{
          console.log(r)
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

</style>
