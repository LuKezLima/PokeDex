<template>
  <div id="app">


    <div class="poke">
<PokeSearch> </PokeSearch>
    </div>

  </div>
    
    
</template>

<script>

import PokeSearch from './components/PokeSearch.vue'

export default {
  name: 'App',
  components: {
    PokeSearch
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  /* margin-top: 60px; */
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: linear-gradient(to right, #ffe259, #ffa751);
}

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.poke{
  width: 100%;
  height: auto;
  background: linear-gradient(to right, #ffe259, #ffa751);
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 10px;
  margin-top: 10px;
}

</style>
