<template>
  <div id="app">

    
   <Search :title="titulo" v-on:search-movie-title="searchMovie"/>
    
   <Content v-bind:movie-title="movieTitleToSearch"/>

    <!-- <div class="row">

      <div class="col-4">
        <Lista/>
      </div>
      <div class="col-8">
         <Crud/> 
      </div>     
   
    </div>        -->
    
  </div>
</template>

<script>
  //import HelloWorld from './components/HelloWorld.vue'
  import Search from './components/Search.vue'
  import Content from './components/Content.vue'
  //import Lista from './components/Lista.vue'
  //import Crud from './components/Crud.vue'

  export default {
    name: 'app',
    components: {
      //HelloWorld,
      Search,
      Content
      //Lista,
      //Crud
    },
    data() {
      return {
        titulo: 'Star Wars Academy',
        movieTitleToSearch: ''
      }
    },
    methods: {
      searchMovie: function (title) {
        // alert(title)
        this.movieTitleToSearch = title
      }
    }
  }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  
}

</style>
