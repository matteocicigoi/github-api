<script>
import axios from 'axios';
import { store } from '../store';
export default {
    data() {
        return {
            store,
            name: '',
            type: 'Repositories'
        }
    },
    methods: {
        search() {
            if(this.name !== ''){
                let url = null;
                if(this.type === 'Repositories'){
                    url = 'https://api.github.com/search/repositories?q=' + this.name;
                }else{
                    url = 'https://api.github.com/search/users?q=' + this.name;
                }
                axios.get(url).then((response) => {
                    this.store.items = response.data.items;
                });
            }
        }
    }   
}
</script>
<template>
    <div class="row align-items-center">
        <div class="col-auto">
            <label for="inputPassword2" class="visually-hidden">Cosa vuoi cercare?</label>
            <input type="text" class="form-control" id="inputPassword2" placeholder="Cosa vuoi cercare?" v-model="name">
        </div>
        <div class="col-auto">
            <select class="form-select" aria-label="Default select example"  v-model="type">
                <option value="Repositories" selected>Repositories</option>
                <option value="Users">Users</option>
            </select>
        </div>
        <div class="col-auto">
            <button type="button" class="btn btn-primary" @click="search()">Cerca</button>
        </div>
    </div>
</template>