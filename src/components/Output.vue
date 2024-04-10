<script>
import { store } from '../store';
export default {
    data() {
        return {
            store
        }
    }
}
</script>
<template>
    <ul>
        <li v-for="item in store.items">{{item.full_name}}</li>
    </ul>
</template>