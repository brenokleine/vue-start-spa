<template>
    <h4>pages</h4>
    <div class="text-end">
        <router-link
            to="/pages/create"
            class="btn btn-primary btn-sm"
        >
            New Page
        </router-link>
    </div>
    <table class="table table-hover">
        <thead>
            <tr>
                <th>
                    Title
                </th>
                <th>
                    Link text
                </th>
                <th>
                    Is published
                </th>
            </tr>
        </thead>
        <tbody>
            <tr 
                v-for="(page, index) in $pages.getAllPages()" 
                :key="index"
                @click="goToPage(index)"
            >
                <td>
                    {{ page.pageTitle }}
                </td>
                <td>
                    {{ page.link.text }}
                </td>
                <td>
                    {{ page.published ? 'yes' : 'no' }}
                </td>
            </tr>
        </tbody>
    </table>
</template>

<script setup>
import { ref, reactive, inject } from 'vue';
import { useRouter } from 'vue-router';

const $pages = inject('$pages')
const router = useRouter();

function goToPage(index){
    router.push(`/pages/${index}/edit`);
}
   
</script>

<style scoped>
    .table.table-hover tr:hover {
        cursor: pointer;
    }
</style>


