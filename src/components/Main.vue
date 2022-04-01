<template>
  <div class="d-flex flex-wrap">
    <FilmCard
    :film="element"
    v-for="(element, index) in mainCards" :key="index"
    />
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
      mainCards: null
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
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import '@/style/main-style.scss';
</style>
