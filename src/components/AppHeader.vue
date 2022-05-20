<template>
  <header class="pt-5 pb-5">
    <div class="container d-flex justify-content-between">
      <div class="logo">Boolflix</div>
      <div class="searcher">
        <input v-model="searchkey" @keyup.enter="seKey()"  placeholder="cerca" type="text">
        <button @click="seKey()">Cerca</button>
      </div>
    </div>
      
  </header>
</template>

<script>
export default {
  name: "AppHeader",
  data() {
    return {
      searchkey: ""
    }
  },
  methods: {
    seKey(){
      this.$emit('search_key', this.searchkey)
    }
  },
}
</script>

<style lang="scss">
button{
  color: black;
}
</style>