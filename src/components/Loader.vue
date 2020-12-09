<template>
    <div class="loader-wrap" v-if="isShowLoader">
        <b-spinner type="grow" variant="light" label="Loading..."></b-spinner>
    </div>
</template>

<script>
import { mapGetters } from 'vuex';

export default {
    name: "Loader",
    computed: {
        ...mapGetters(["isShowLoader"])
    }
};
</script>

<style lang="scss">
    .loader-wrap {
        position: fixed;
        width: 100%;
        height: 100%;
        left: 0;
        top: 0;
        background-color: rgba($color: #000000, $alpha: 0.7);
        display: flex;
        align-items: center;
        justify-content: center;
        z-index: 999;
    }
</style>