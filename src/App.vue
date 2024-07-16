<template>
    <navbar></navbar>

    <router-view></router-view>

</template>

<script>
import PageViewer from './components/PageViewer.vue'
import Navbar from './components/Navbar.vue'
import CreatePage from './components/CreatePage.vue'

export default {
    components: {
        PageViewer,
        Navbar,
        CreatePage
    },
    methods: {
        pageCreated(pageObj){
            this.pages.push(pageObj);
            
        }
    },
    
}
</script>