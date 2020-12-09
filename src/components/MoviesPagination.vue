<template>
    <div class="movies-pagination">
        <b-pagination v-model="currentPageModel" :per-page="perPage" :total-rows="total" prev-text="Prev" next-text="Next">

        </b-pagination>
    </div>
</template>

<script>
export default {
    name: 'MoviesPagination',
    props: {
        currentPage: {
            type: Number,
            default: 1
        },
        total: {
            type: Number,
            default: 1
        },
        perPage: {
            type: Number,
            default: 1
        }
    },

    computed: {
        currentPageModel: {
            get() {
                return this.currentPage;
            },
            set(value) {
                this.$emit('pageChanged', value);
            }
        }
    }
};
</script>

<style lang="scss">
    .movies-pagination {
        display: flex;
        justify-content: center;
        margin-top: 30px;
        & > .pagination > .page-item > .page-link {
            background-color: transparent;
            font-size: 18px;
            color: #ffffff;
            box-shadow: none;
        } 
        & > .pagination > .page-item.active > .page-link{
            border-color: #ffffff;
            background-color: #ffffff;
            color: #000000;
        }
        & > .pagination > .page-item.disabled > .page-link {
            color: lightgray;
        }
    }
</style>