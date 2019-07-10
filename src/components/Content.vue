<template>
<div class="content">
    <div class="container">
      <br><br>

       <h2 style="text-align:left">Listado</h2> 

      <h3>{{movieTitle}}</h3>
      
      <table class="table table-bordered table-hover">
        <thead>
            <th>Título</th>
            <th>Episodio</th>
            
        </thead>
        <tbody>
            <tr v-for="movie in movies.results" v-bind:key="movie.episode_id">
                <td>{{movie.title}}</td>
                <td>{{movie.episode_id}}</td>              
                
            </tr>                        
        </tbody>               
      </table>
      <br><br>
    </div>

    <div class="row">
      <div class="container">
        
        <div class="col-8" align="left">
          <form action="" class="text-left">
            <!-- <div class="form-group">
              <label >ID</label>
              <input v-model="id" type="text" class="form-control" id="id" placeholder="ID">
            </div> -->
            <div class="form-group">
              <label >Título</label>
              <input v-model="Title" type="text" class="form-control" id="Title" placeholder="Título">
            </div>
            <div class="form-group">
              <label >Año</label>
              <input v-model="Year" type="text" class="form-control" id="Year" placeholder="Año">
            </div>
            <div class="form-group">
              <label >Edad</label>
              <input v-model="Age" type="text" class="form-control" id="Age" placeholder="Edad">
            </div>   
            <div class="form-group">
              <label >Idioma</label>
              <input v-model="Language" type="text" class="form-control" id="Language" placeholder="Idioma">
            </div>         
              <input @click="addMovie" type="button" value="Guardar" class="btn btn-primary">
          </form>
          
        </div>  
      </div>     
    </div>
    <br/><br/>
  
  </div>
</template>

<script>
export default {
  props: ['movieTitle'],
  data() {
    return {      
      Title:'',
      Year:'',
      Age:'',
      Language:'',
      movies: [],
      newMovie:[]
    }
  },
  mounted() {
    if ( localStorage.getItem( 'movies' ) ) {
      try {
        this.movies = JSON.parse( localStorage.getItem( 'movies' ) )
        // eslint-disable-next-line
        console.log( 'movies obtenidas de localStorage' )
      } catch( error ) {
        localStorage.removeItem( 'movies' )
        this.loadCatalog().catch( e => alert( e.message ) )
      }
    } else {
      this.loadCatalog().then( () => this.saveMovies() ).catch( e => alert( e.message ) )
    }
  },
  methods: {
    loadCatalog: async function() {
      try {
        const data = await fetch( 'https://swapi.co/api/films/' )
        this.movies = await data.json()
      } catch ( error ) {
        throw error
      }
    },    
    addMovie() {      
         
      this.movies.push({
        id: + new Date,
        Title: this.Title,
        Age: this.Age,
        Year: this.Year,
        Language: this.Language
      });
      this.saveMovies(); 
      this.Title = '';
      this.Age = ''; 
      this.Year = ''; 
      this.Language = '';          
      
    },
    saveMovies() {
      const parsed = JSON.stringify( this.movies )
      localStorage.setItem( 'movies', parsed )
    }    
  },
    computed: {
    filteredMovies() {
      // return this.movies.filter( movie => movie.Title == this.movieTitle)
      /*    
      The indexOf() method returns the position of the first occurrence of a specified value in a string.
      This method returns -1 if the value to search for never occurs.
      Note: The indexOf() method is case sensitive. 
      https://www.w3schools.com/jsref/jsref_indexof.asp
      */
      return this.movies.filter( (movie) =>
        movie.Title.toLowerCase().indexOf(this.movieTitle.toLowerCase()) > -1
      )
    }
  }
}
</script>