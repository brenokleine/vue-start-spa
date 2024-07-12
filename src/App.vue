<template>
    <navbar
        :pages="pages"
        :activePage="activePage"
        :nav-link-click="(index) => activePage = index"
    >
    </navbar>

    <!-- <page-viewer
        v-if="pages.length > 0"
        :page="pages[activePage]"
    >
    </page-viewer> -->

    <create-page
        :page-created="pageCreated"
    >
    </create-page>

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
    data() {
        return {
            activePage: 0,
            pages: []
        }
    },
    created() {
        this.getPages();
    },
    methods: {
        async getPages() {
            let res = await fetch('pages.json');
            let data  = await res.json();

            this.pages = data;
        },
        pageCreated(pageObj){
            this.pages.push(pageObj);
            
        }
    }
}
</script>