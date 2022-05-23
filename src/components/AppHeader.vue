<template>
  <header class="pt-5 pb-5">
    <div class="container d-flex justify-content-between align-items-center">
      <img class="logo"  @click="seKey('')" src="../assets/img/logo.png" alt="">
      <div class="align-items-end">

        <h3 :class=" settedLib === 'all' ? 'underline' : '' " @click="setlibrary('all')" class="d-inline-block ml-5">Tutti</h3>
        <h3 :class=" settedLib === 'movie' ? 'underline' : '' " @click="setlibrary('movie')" class="d-inline-block mx-5">Film</h3>
        <h3 :class=" settedLib === 'tv' ? 'underline' : '' " @click="setlibrary('tv')" class="d-inline-block ">Serie TV</h3>
      </div>
      <div class="searcher">
        <input v-model="searchkey" @keyup.enter="seKey()"   placeholder="cerca" type="text">
        <button @click="seKey()" class="btn btn-danger">Cerca</button>
      </div>
    </div>
      
  </header>
</template>

<script>
export default {
  name: "AppHeader",
  data() {
    return {
      searchkey: "",
      settedLib: "all"
    }
  },
  methods: {
    setlibrary(param){
        this.$emit('search_lib', param )
        this.settedLib = param
    },
    seKey(param){
      if(param === ""){
        this.searchkey = ""
        this.$emit('search_key',this.searchkey )
      }else{
        this.$emit('search_key', this.searchkey)
      }
    }
  },
}
</script>

<style lang="scss" scoped>
h3{
  font-weight: bold;
  cursor: pointer;
}

.underline{
  text-decoration: underline;
}

.logo{
  width: 14vw;
  cursor: pointer;
}
input{
  padding: 5px 10px;
  border-top-left-radius: 8px;
  border-bottom-left-radius: 8px;
  border-color: black;

}

button{
  // background-color: rgb(44, 44, 44);
  // border-color: rgb(42, 42, 42);
  // border-top-right-radius: 8px;
  // border-bottom-right-radius: 8px;
  // padding: 6px 10px;
  margin-bottom:5px ;
}
</style>