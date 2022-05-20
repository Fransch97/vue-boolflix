<template>
  <header class="pt-5 pb-5">
    <div class="container d-flex justify-content-between">
      <div class="logo">Boolflix</div>
      <input v-model="searchkey" @keyup.enter="$emit('search_key', searchkey)"  placeholder="cerca" type="text">
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
}
</script>

<style lang="scss">

</style>