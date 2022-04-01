<template>
<div class="p-5">
  <input type="text" class="farm-control m-5" placeholder="Inserisci film" v-model="filmToSearch">
  <button class="btn btn-primary">Cerca</button>
  <div class="d-flex flex-wrap">
    <FilmCard
    :film="element"
    v-for="(element, index) in fileteredFilms" :key="index"
    />
  </div>
</div>
</template>

<script>
import axios from 'axios'
import FilmCard from './FilmCard.vue'
export default {
  name: 'IndexMain',
  components: {
    FilmCard,
  },
  data: function(){
    return{
      mainCards: null,
      filmToSearch: '',
      filmFilter: null,
    }
  },
  created: function(){
    this.getApiInfo();
  },
  methods: {
      getApiInfo() {
        axios
      .get('https://api.themoviedb.org/3/movie/top_rated?api_key=291efde9ec311b454fd9de73cb4e8f5c&language=en-US&page=1')
      .then((result) =>{
        this.mainCards = result.data.results;
        console.log(this.mainCards);
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
                return this.mainCards;
            }
        return this.mainCards.filter(
                (element) => element.title.toLowerCase().includes(this.filmToSearch.toLowerCase().trim())
      );
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import '@/style/main-style.scss';
</style>
