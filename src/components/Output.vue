<script>
import { store } from '../store';
import Element from './Element.vue';
export default {
    data() {
        return {
            store,
        }
    },
    components : {
        Element
    },
}
</script>
<template>
    <div class="row gap-5 justify-content-center">
        <template v-for="item in store.items">
            <template v-if="item.type">
                <Element v-for="item in store.items" :name="item.login" :link="item.html_url" :description="item.type" :star="0" :img="item.avatar_url"/>
            </template>
            <template v-else>
                <Element v-for="item in store.items" :name="item.full_name" :link="item.html_url" :description="item.description" :star="item.stargazers_count" :img="item.owner.avatar_url"/>
            </template>
        </template>
    </div>
</template>