<template>
    <header class="header">
        <b-navbar type="dark" variant="dark" class="header__nav">
            <b-container>
                <b-navbar-brand href="#">MovieDB</b-navbar-brand>
                <b-nav-form>
                <b-form-input class="mr-sm-2 header__search" placeholder="Search" v-model="searchValue" debounce="500"></b-form-input>
                </b-nav-form>
            </b-container>
        </b-navbar>
    </header>
</template>

<script>
import {mapActions} from 'vuex';

export default {
    name: "Header",
    data: () => ({ 
        searchValue: ''
    }),
    watch: {
        searchValue: 'onSearchValueChanged'
    },
    methods: {
        ...mapActions('movies', ['searchMovies', 'fetchMovies', 'toggleSearchState']),
        onSearchValueChanged(val) {
            console.log(val);
            if (val) {
                this.searchMovies(val);
                this.toggleSearchState(true);
            } else {
                this.fetchMovies();
                this.toggleSearchState(false);
            }
            
        }
    }
};
</script>

<style lang="scss">
    .header {
        margin: 20px;
        &__nav{
            background-color: rgba($color: #000000, $alpha: 0.7) !important;
        }
        &__search {
            color: #ffffff;
            background: rgba($color: #928383, $alpha: 0.1);
            border-color: rgba($color: #000000, $alpha: 0.6);
        }
    }
</style>