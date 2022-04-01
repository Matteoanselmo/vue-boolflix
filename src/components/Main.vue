<template>
<div class="px-4 pb-4">
  <input type="text" class="farm-control shadow-lg mb-4" placeholder="Cerca Film/Serie" v-model="filmToSearch">
  <span class="flag-icon flag-icon-squared flag-icon-uk"></span>
  <div class="d-flex flex-wrap" v-if="(filmToSearch != '')">
    <FilmCard
    v-for="(element, index) in fileteredFilms" :key="index"
    :film="element"
    />
    <SerieCard 
    v-for="(serie, index) in fileteredSeries" :key="index"
    :serie="serie"
    />
  </div>
  
</div>
</template>

<script>
import axios from 'axios'
import FilmCard from './FilmCard.vue'
import SerieCard from './SerieCard.vue'
import FlagIcon from 'vue-flag-icon'
import Vue from 'vue';
Vue.use(FlagIcon);
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
  created: function(){
    this.getFilmInfo();
    this.getSerieInfo();
  },
  methods: {
      getFilmInfo() {
        axios
      .get('https://api.themoviedb.org/3/movie/top_rated?api_key=291efde9ec311b454fd9de73cb4e8f5c&language=en-US')
      .then((result) =>{
        this.mainFilmCards = result.data.results;
        console.log(this.mainFilmCards);
      })
      .catch((error) => {
        console.error(error);
      })
    },
    getSerieInfo() {
        axios
      .get('https://api.themoviedb.org/3/search/tv?api_key=e99307154c6dfb0b4750f6603256716d&language=it_IT&query=scrubs')
      .then((result) =>{
        this.mainSerieCards = result.data.results;
        console.log(this.mainSerieCards);
      })
      .catch((error) => {
        console.error(error);
      })
    }
  },
  computed: {
      fileteredFilms(){
        if ( this.filmToSearch.toLowerCase().trim() === ''){
                console.warn('Stai cercando una stringa vuota');
                return this.mainFilmCards;
            }
        return this.mainFilmCards.filter(
                (element) => element.title.toLowerCase().includes(this.filmToSearch.toLowerCase().trim())
      );
    },
    fileteredSeries(){
        if ( this.filmToSearch.toLowerCase().trim() === ''){
                console.warn('Stai cercando una stringa vuota');
                return this.mainSerieCards;
            }
        return this.mainSerieCards.filter(
                (element) => element.name.toLowerCase().includes(this.filmToSearch.toLowerCase().trim())
      );
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import '@/style/main-style.scss';
</style>
