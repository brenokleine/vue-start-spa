<template>
    <navbar
        :pages="pages"
        :activePage="activePage"
        :nav-link-click="(index) => activePage = index"
    >
    </navbar>

    <page-viewer
        v-if="pages.length > 0"
        :page="pages[activePage]"
    >
    </page-viewer>
</template>

<script>
import PageViewer from './components/PageViewer.vue'
import Navbar from './components/Navbar.vue'

export default {
    components: {
        PageViewer,
        Navbar
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
        }
    }
}
</script>