<template>
    <div>
        <div class="card text-white mb-3 mx-2 p-3 shadow-lg" style="width: 18rem;">
            <img :src="`https://image.tmdb.org/t/p/w500${film.poster_path}`" class="card-img-top" :alt="film.name">
            <div class="card-body">
                <h5 class="card-title">FILM: {{ film.title }}</h5>
                <h6 class="card-title">{{ film.original_title }}</h6>
                <!-- <p class="card-text">{{ film.overview }}</p> -->
                <h6 class="card-title">Original lenguage: {{ film.original_language }}</h6>
                <a href="#" class="btn btn-primary">{{ film.vote_average }}</a>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'FilmCard',
    props: { 'film' : Object },
    data: function(){
        return{
            country: ''
        }
    },
    created: function(){
        this.countryToSearch();
    },
    methods: {
        countryToSearch(){
            if(this.film.original_language == 'es'){
                this.country = 'https://upload.wikimedia.org/wikipedia/commons/thumb/9/9a/Flag_of_Spain.svg/2560px-Flag_of_Spain.svg.png';
            }else if (this.film.original_language == 'en'){
                this.country = 'https://upload.wikimedia.org/wikipedia/commons/thumb/3/30/Flag_of_the_United_Kingdom_%283-2_aspect_ratio%29.svg/1200px-Flag_of_the_United_Kingdom_%283-2_aspect_ratio%29.svg.png';
            }else if (this.film.original_language == 'zh'){
                this.country = 'https://www.crwflags.com/fotw/images/c/ch-zh.gif';
            }else if(this.film.original_language == 'ko'){
                this.country = 'https://upload.wikimedia.org/wikipedia/commons/thumb/2/28/Flag_of_South_Korea_%281945%E2%80%931948%29.svg/2560px-Flag_of_South_Korea_%281945%E2%80%931948%29.svg.png';
            }
        }
    }
}

</script>

<style lang="scss"> 
    .card{
        background-color: #1E2D3B !important;
        // height: 400px !important;
    }

</style>