<template>
    <div class="poster-page" :style="posterStyle"></div>
</template>


<script>
export default {
    name: "PosterBg",
    props: {
        poster: {
            type: String,
            default: ""
        }
    },
    data: () => ({
        defaultPosterBg: 'linear-gradient(52deg, #2b4c59, #988080)'
    }),
    computed: {
        posterStyle() {
            return {
                'background-image': this.posterBg
            };
        },
        posterBg() {
            return this.poster ? `url(${this.poster})` : this.defaultPosterBg;
        }
    }
};
</script>


<style lang="scss">
    .poster-page {
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        z-index: -1;
         
         background-size: 150% 150%;
        animation: AnimationPoster 30s ease infinite;
        &::before{
            content: "";
            position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        opacity: 0.6;
        background-image: linear-gradient(52deg, #2b4c59, #988080);
        }
    }

    @keyframes AnimationPoster {
    0%{background-position:0% 50%}
    50%{background-position:100% 50%}
    100%{background-position:0% 50%}
}
</style>