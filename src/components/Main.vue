<template>
<div class="px-4 pb-4">
  <div class="d-flex justify-content-between netflix-search">
    <h1 class="text-danger text-uppercase m-4 shadow-lg" >boolflix</h1>
    <input type="text" class="farm-control shadow-lg m-4" placeholder="Cerca Film/Serie" v-model="filmToSearch" @keydown.enter="getFilmInfo(filmToSearch), getSerieInfo(filmToSearch), filmToSearch = ''">
  </div>
  <div class="d-flex my-card-wrapper"  >
    <FilmCard
    v-for="(element, index) in mainFilmCards" :key="index"
    :film="element"
    />
    <SerieCard 
    v-for="(serie, index) in mainSerieCards" :key="'a' + index"
    :serie="serie"
    />
  </div>
  
</div>
</template>

<script>
import axios from 'axios';
import FilmCard from './FilmCard.vue';
import SerieCard from './SerieCard.vue';

export default {
  name: 'IndexMain',
  components: {
    FilmCard,
    SerieCard
  },
  data: function(){
    return{
      mainFilmCards: null,
      mainSerieCards: null,
      filmToSearch: '',
      filmFilter: null,
      serieFilter: null,
    }
  },
  // created: function(){
  //   this.getFilmInfo();
  //   this.getSerieInfo();
  // },
  methods: {
      getFilmInfo(film) {
        axios
      .get(`https://api.themoviedb.org/3/search/movie?api_key=291efde9ec311b454fd9de73cb4e8f5c&language=en-US&page=1&query=${film}`)
      .then((result) =>{
        this.mainFilmCards = result.data.results;
        console.log(this.mainFilmCards);
      })
      .catch((error) => {
        console.error(error);
      })
    },
    getSerieInfo(serieApi) {
        axios
      .get(`https://api.themoviedb.org/3/search/tv?api_key=291efde9ec311b454fd9de73cb4e8f5c&language=en-US&page=1&query=${serieApi}`)
      .then((result) =>{
        this.mainSerieCards = result.data.results;
        console.log(this.mainSerieCards);
      })
      .catch((error) => {
        console.error(error);
      })
    }
  },
  // computed: {
  //     fileteredFilms(){
  //       if ( this.filmToSearch.toLowerCase().trim() === ''){
  //               console.warn('Stai cercando una stringa vuota');
  //               return this.mainFilmCards;
  //           }
  //       return this.mainFilmCards.filter(
  //               (element) => element.title.toLowerCase().includes(this.filmToSearch.toLowerCase().trim()),
                
  //     );
  //   },
  //   fileteredSeries(){
  //       if ( this.filmToSearch.toLowerCase().trim() === ''){
  //               console.warn('Stai cercando una stringa vuota');
  //               return this.mainSerieCards;
  //           }
  //       return this.mainSerieCards.filter(
  //               (element) => element.name.toLowerCase().includes(this.filmToSearch.toLowerCase().trim()),
                
  //     );
  //   }
  //}
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import '@/style/main-style.scss';
.netflix-search{
  position: fixed;
  top: 14px;
  width: 95vw;
  input{
    height: 2rem;
  }
}
.my-card-wrapper{
  margin-top: 7rem;
}
</style>
