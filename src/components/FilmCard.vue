<template>
    <div>
        <div class="card" style="width: 18rem;">
            <img :src="''" class="card-img-top" :alt="film.title">
            <div class="card-body">
                <h5 class="card-title">{{ film.title }}</h5>
                <h6 class="card-title">{{ film.original_title }}</h6>
                <p class="card-text">{{ film.original_language }}</p>
                <a href="#" class="btn btn-primary">{{ film.vote_average }}</a>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'FilmCard',
    props: { 'film' : Object }
}
</script>

<style>

</style>