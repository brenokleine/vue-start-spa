<template>
    <div class="container" v-if="page">
        <h1>{{page.pageTitle}}</h1>
        <p>{{page.content}}</p>
    </div>
</template>

<script>
export default {
    props: ['index'],
    inject: ['$pages'],
    created(){
        this.page = this.$pages.getSinglePage(this.index);
    },
    data(){
        return {
            page: null
        }
    },
    watch: {
        index(newIndex, oldIndex){
            this.page = this.$pages.getSinglePage(newIndex);
        }
    }
    
}
</script>