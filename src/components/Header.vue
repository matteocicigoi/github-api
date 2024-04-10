<script>
import Search from './Search.vue';
export default {
    components: {
        Search
    }
}
</script>
<template>
    <header>
        <nav class="navbar bg-body-tertiary">
            <div class="container-fluid">
                <span class="navbar-brand mb-0 h1">GitHub Api</span>
                <Search />
            </div>
        </nav>
    </header>
</template>