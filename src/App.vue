<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <h1>What Movie Would You Like to Find?</h1>
   <section class="inputbox"> 
    <input v-model="searchTerm" placeholder="Search">
    <br>
    <button v-on:click="searchTerm"> Submit </button>
    <br>
    <img src="http://placepuppy.net/400/250">
  </section>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: "app",
  components: {},
  data: function() {
    return {
      searchTerm: ""
    };
  },
  methods:{
  searchTerm:function() {
    console.log(this.searchTerm);
      const URL = `https://api.themoviedb.org/3/search/movie?api_key=9fe2614f2b9d0f56b7e758ac2b8ef828&language=en-US&query=${
        this.search
      }&page=1&include_adult=false`;
      fetch(URL)
        .then(resp => resp.json())
        .then(json => {
          console.log(json);
          this.movies=json.results
        });
    },
    getImageURL(poster_path) {
      return "https://image.tmdb.org/t/p/w500/" + poster_path;
    }
  }
};

</script>

<style>
.inputbox {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
}
</style>
