<template>
    <b-container>
        <h2>{{ listTitle }}</h2>
        <b-row>
            <template v-if="isExist">
                <b-col cols="3" v-for="(movie, key) in list" :key="key">
                    <MovieItem :movie="movie" @mouseover.native="onMouseOver(movie.Poster)" @removeItem="onRemoveItem" @showModal="onShowMovieInfo"/>
                </b-col>
            </template>
            <template v-else>
                <div>
                    Empty list
                </div>
            </template>
        </b-row>
        <b-modal body-class="movie-body" :id="movieInfoModalID" size="xl" hide-header hide-footer>
            <MovieInfoModalContent :movie="selectedMovie" @closeModal="onCloseModal"/>
        </b-modal>
    </b-container>
</template>

<script>

import {mapActions, mapGetters} from 'vuex';
import MovieItem from "./MovieItem"
import MovieInfoModalContent from "./MovieInfoModalContent"

export default {
    name: "MoviesList",
    props: {
        list: {
            type: Object,
            default: () => ({})
        }
    },
    data: () => ({
        movieInfoModalID: "movie-info",
        selectedMovieID: ""
    }),
    components: {
        MovieItem,
        MovieInfoModalContent
    },
    computed: {
        ...mapGetters('movies', ['isSearch']),
        isExist() {
            return Boolean(Object.keys(this.list).length);
        },
        listTitle(){
            return this.isSearch? "Search result" : "Movie List";
        },
        selectedMovie(){
            return this.selectedMovieID ? this.list[this.selectedMovieID] : null;
        }
    },
    methods: {
        ...mapActions('movies', ['removeMovie']),
        ...mapActions(["showNotify"]),
        onMouseOver(poster) {
            this.$emit('changePoster', poster);
        },
        async onRemoveItem({ id, title }){
            const isConfirmed = await this.$bvModal.msgBoxConfirm(`Are you sure you want to delete ${title} ?`);
            
            if (isConfirmed) {
                this.removeMovie(id);
                this.showNotify({
                    msg: "Movie deletet successful",
                    variant: "success",
                    title: "Success"

                })
            }
        },
        onShowMovieInfo(id) {
            this.selectedMovieID = id;
            this.$bvModal.show(this.movieInfoModalID);

        },
        onCloseModal(){
            this.selectedMovieID = null;
            this.$bvModal.hide(this.movieInfoModalID);
        }
    }
};
</script>

<style lang="scss">
    h2 {
        color: #ffffff;
        margin-bottom: 20px;
    }
   .movie-body{
       padding: 0 !important
   }
   
</style>
