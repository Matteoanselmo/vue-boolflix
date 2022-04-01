<template>
    <div>
        <div class="card text-white mb-3 mx-2 p-3 shadow-lg" style="width: 18rem;">
            <img :src="country" class="card-img-top" :alt="serie.name">
            <div class="card-body">
                <h5 class="card-title">{{ serie.name }}</h5>
                <h6 class="card-title">{{ serie.original_name }}</h6>
                <p class="card-text">{{ serie.overview }}</p>
                <a href="#" class="btn btn-primary">{{ serie.vote_average }}</a>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'SerieCard',
    props: { 'serie' : Object },
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
            if(this.serie.original_language == 'ja'){
                this.country = 'https://upload.wikimedia.org/wikipedia/commons/thumb/9/9e/Flag_of_Japan.svg/280px-Flag_of_Japan.svg.png';
            }else if (this.serie.original_language == 'en'){
                this.country = 'https://upload.wikimedia.org/wikipedia/commons/thumb/3/30/Flag_of_the_United_Kingdom_%283-2_aspect_ratio%29.svg/1200px-Flag_of_the_United_Kingdom_%283-2_aspect_ratio%29.svg.png';
            }else if (this.serie.original_language == 'hi'){
                this.country = 'https://upload.wikimedia.org/wikipedia/commons/thumb/e/ef/Flag_of_Hawaii.svg/1280px-Flag_of_Hawaii.svg.png';
            }else if(this.serie.original_language == 'ko'){
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