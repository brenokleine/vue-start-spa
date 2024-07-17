<template>
    <div class="container mb-3">
        <form action="">
            <div class="row p-4">
                <div class="col-md-8">
                    <div class="mb-3">
                        <label for="" class="form-label">
                            Page Title
                        </label>
                        <input type="text" class="form-control" v-model="pageTitle" />
                    </div>
                    <div class="mb-3">
                        <label for="" class="form-label">
                            Content
                        </label>
                        <textarea type="text" class="form-control" rows="5" v-model="content"></textarea>
                    </div>
                </div>
                <div class="col">
                    <div class="mb-3">
                        <label for="" class="form-label">
                            Link Text
                        </label>
                        <input type="text" class="form-control" v-model="linkText"/>
                    </div>
                    <div class="row mb-3">
                        <div class="form-check">
                            <input class="form-check-input" type="checkbox" v-model="published">
                            <label class="form-check-label" for="gridCheck1">
                                Published
                            </label>
                        </div>
                    </div>
                </div>
            </div>
            <div class="mb-3">
                <button class="btn btn-primary" @click.prevent="submitForm" :disabled="isFormInvalid">
                    Create Page
                </button>
            </div>
        </form>
    </div>
</template>

<script setup>
import {ref, inject, computed, watch} from 'vue';
import { useRouter } from 'vue-router';

const router = useRouter();

const bus = inject('$bus');
const pages = inject('$pages');

let pageTitle = ref('');
let content = ref('');
let linkText = ref('');
let published = ref(true);
//refs are objects with this structure: {value: 'some value'}

function submitForm(){
    if (!pageTitle || !content || !linkText) {
        alert('Please fill out all fields');
        return;
    }

    let newPage = {
        pageTitle: pageTitle.value,
        content: content.value,
        link: {
            text: linkText.value,
        },
        published: published.value,
    }

    pages.addPage(newPage)

    bus.$emit('page-created', newPage)

    router.push(`/pages`)
}

const isFormInvalid = computed(() => {
    return !pageTitle || !content || !linkText;
})

//thing to be watched has to be reactive (ref or reactive)
watch(pageTitle, (newTitle, oldTitle) => {
    if (linkText.value === oldTitle) {
        linkText.value = newTitle;
    }
})
</script>