<script>
import { store } from '../store';
import Element from './Element.vue';
export default {
    data() {
        return {
            store,
        }
    },
    components: {
        Element
    },
}
</script>
<template>
    <div class="row gap-5 justify-content-center" v-if="store.items !== null && store.items !== '0'">
        <template v-for="item in store.items">
            <template v-if="item.type">
                <Element :name="item.login" :link="item.html_url" :description="item.type" :star="0"
                    :img="item.avatar_url" />
            </template>
            <template v-else>
                <Element :name="item.full_name" :link="item.html_url" :description="item.description"
                    :star="item.stargazers_count" :img="item.owner.avatar_url" />
            </template>
        </template>
    </div>
    <div class="alert alert-info container mt-5 text-center" role="alert" v-else-if="store.items === '0'">
        Non ci sono risultati
    </div>
    <div class="spinner-border text-primary border-5" style="width: 100px; height: 100px; margin-top: 50px; margin-left: calc(50% - 50px)" role="status" v-if="store.find === false">
        <span class="visually-hidden">Loading...</span>
    </div>
</template>