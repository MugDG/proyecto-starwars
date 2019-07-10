<template>
  <div class="search">

    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a href="/" class="navbar-brand">{{title}}</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          
         
          <li class="nav-item dropdown">
            <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
              Categorías
            </a>
            <div class="dropdown-menu" aria-labelledby="navbarDropdown">
              <a class="dropdown-item" href="#">CAT A</a>
              <a class="dropdown-item" href="#">CAT B</a>
              
            </div>
          </li>
          
        </ul>
        <form class="form-inline my-2 my-lg-0" @submit.prevent="search">
          <input v-model="titleSearch" class="form-control mr-sm-2" type="search" placeholder="Buscar" aria-label="Buscar">
          <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Buscar</button>
        </form>
      </div>
    </nav>
  </div>
    
</template>

<script>
  export default {
    name: 'Search', 
    props: ['title'],   
    data(){
      return{
        titleSearch:''
      }
    },
    methods:{
      search() {
      this.$emit('search-movie-title', this.titleSearch)
      // console.log('aaa')
      }
    }    
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
