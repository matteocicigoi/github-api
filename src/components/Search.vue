<script>
import axios from 'axios';
import { store } from '../store';
export default {
    data() {
        return {
            store,
            name: ''
        }
    },
    methods: {
        search() {
            if(this.name !== ''){
                axios.get('https://api.github.com/search/repositories?q=' + this.name).then((response) => {
                    this.store.items = response.data.items;
                });
            }
        }
    }   
}
</script>
<template>
    <form class="row g-3">
        <div class="col-auto">
            <label for="inputPassword2" class="visually-hidden">Cosa vuoi cercare?</label>
            <input type="text" class="form-control" id="inputPassword2" placeholder="Cosa vuoi cercare?" v-model="name">
        </div>
        <div class="col-auto">
            <select class="form-select" aria-label="Default select example">
                <option selected>Repository</option>
                <!--<option value="1">One</option>-->
            </select>
        </div>
        <div class="col-auto">
            <button type="button" class="btn btn-primary mb-3" @click="search()">Cerca</button>
        </div>
    </form>
</template>