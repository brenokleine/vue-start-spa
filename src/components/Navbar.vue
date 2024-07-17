<template>
    <nav :class="[`navbar-${theme}`, `bg-${theme}`, 'navbar', 'navbar-expand-lg']">
        <div class="container-fluid">
            <a class="navbar-brand" href="#">My Vue</a>
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">               
                <navbar-link 
                    v-for="(page, index) in publishedPages" class="nav-item" :key="index"
                    :page="page"
                    :index="index"
                >
                </navbar-link>   
                
                <li>
                    <router-link
                        to="/pages"
                        class="nav-link"
                        aria-current="page"
                        active-class="active"
                    >
                        Pages
                    </router-link>
                </li>
            </ul>
            <form class="d-flex">
                <button class="btn btn-primary" @click.prevent="changeTheme()">Toggle</button>
            </form>
        </div>
    </nav>
</template>

<script>
import NavbarLink from './NavbarLink.vue';

export default {
    data(){
        return {
            theme: 'dark',
            pages: []
        }
    },
    inject: ['$pages', '$bus'],
    components: {
        NavbarLink
    },
    computed:{
        publishedPages(){
            return this.pages.filter(page => page.published);
        }
    },
    created(){
        this.getThemeSetting();

        this.pages = this.$pages.getAllPages();

        this.$bus.$on('page-updated', () => {
            this.pages = [...this.$pages.getAllPages()];
        })

        this.$bus.$on('page-created', () => {
            this.pages = [...this.$pages.getAllPages()];
        })

        this.$bus.$on('page-deleted', () => {
            this.pages = [...this.$pages.getAllPages()];
        })
    },
    methods: {
        changeTheme(){
            this.theme = this.theme === 'dark' ? 'light' : 'dark'

            this.storeThemeSetting();
        },
        storeThemeSetting(){
            localStorage.setItem('theme', this.theme);
        },
        getThemeSetting() {
            let theme = localStorage.getItem('theme');

            if(theme){
                this.theme = theme;
            }
        },
    }
}
</script>