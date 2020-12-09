<template>
    <div class="movie-item mb-3">
        <div class="movie-item__poster" :style="posterBg"></div>
        <div class="movie-item__wrap">
            <div class="movie-item__info">
                <h3 class="movie-item__info_title">{{ movie.Title }}</h3>
                <span class="movie-item__info_year">{{ movie.Year }}</span>    
            </div> 
            <div class="movie-item__controls row no-gutters">
                <div class="col pr-2">
                    <b-button size="md" block variant="outline-light" @click="showInfoModalEvent">Info</b-button>
                </div>
                <div class="col pl-2">
                    <b-button size="md" block variant="outline-light" @click="emitRemoveEvent">Remove</b-button>
                </div>
            </div>
        </div>

    </div>
</template>

<script>
export default {
    name: "MovieItem",
    props: {
        movie: {
            type: Object,
            required: true
        }
    },
    computed: {
        posterBg() {
            return {
                'background-image': `url(${this.movie.Poster})`
            }
        }
    },
    methods: {
        emitRemoveEvent(){
            this.$emit('removeItem', {id: this.movie.imdbID, title: this.movie.Title});
        },
        showInfoModalEvent() {
            this.$emit('showModal', this.movie.imdbID);

        }
    }
};
</script>

<style lang="scss">
    .movie-item{
        position: relative;
        cursor: pointer;
        border-radius: 5px;
        overflow: hidden;
        transition: .2s ease;
        height: 400px;
        &:hover {
            box-shadow: -3px 1px 26px -1px rgba(0,0,0,.3);
            transform: scale(1.02);
            transition: .3s ease;
        }
        &:hover .movie-item__wrap{
            opacity: 1;
            background-color: rgba(0,0,0,.6);
        }
        &__poster {
            position: absolute;
            top: 0;
            left: 0;
            bottom: 0;
            right: 0;
            background-repeat: no-repeat;
            background-size: cover;
            background-position: center;
            z-index: -1;
        }
        &__wrap {
            padding: 10px;
            height: 100%;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            opacity: 0;
            transition: .2s ease;
        }
        &__info{
            &_title {
                font-size: 22px;
                color: #ffffff;
            }
            &_year {
                font-size: 16px;
                color: #ffffff;
            }
        }
    }
</style>