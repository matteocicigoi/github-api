<script>
import axios from 'axios';
import { store } from '../store';
export default {
    data() {
        return {
            store,
            name: '',
            type: 'Repositories',
            debounceTimer : null
        }
    },
    methods: {
        search() {
            if (this.name.length >= 3) {
                // se il nome è maggiore di 3 caratteri
                let url = null;
                if (this.type === 'Repositories') {
                    // se la categoria è repositories
                    url = 'https://api.github.com/search/repositories?q=' + this.name;
                } else {
                    // altrimenti un user
                    url = 'https://api.github.com/search/users?q=' + this.name;
                }
                // attiva il caricamento e fa la chiamata api
                this.store.find = false;
                this.store.items = null;
                axios.get(url).then((response) => {
                    if (response.data.items.length === 0) {
                        // se non ci sono risultati
                        this.store.items = '0';
                    } else {
                        this.store.items = response.data.items;
                    }
                }).finally((response) => {
                    // disattiva il caricamento
                    this.store.find = true;
                });
            }
        },
        delayedSearch() {
            // se l'utente smette di digitare
            clearTimeout(this.debounceTimer);
            this.debounceTimer = setTimeout(() => {
                this.search();
            }, 700);
        }
    }
}
</script>
<template>
    <div class="row align-items-center">
        <div class="col-auto">
            <label for="inputPassword2" class="visually-hidden">Cosa vuoi cercare?</label>
            <input type="text" class="form-control" id="inputPassword2" placeholder="Cosa vuoi cercare?" v-model="name"
                @input="delayedSearch()">
        </div>
        <div class="col-auto">
            <select class="form-select" aria-label="Default select example" v-model="type">
                <option value="Repositories" selected>Repositories</option>
                <option value="Users">Users</option>
            </select>
        </div>
        <div class="col-auto">
            <button type="button" class="btn btn-primary" @click="search()">Cerca</button>
        </div>
    </div>
</template>