<script>
export default {
    props: ['name', 'link', 'description', 'star', 'img'],
};
</script>
<template>
    <!-- Singolo elemento -->
    <div class="card p-0 col-12 col-sm-5 col-lg-3 col-xxl-2">
        <div class="card-header"
            :class="{ 'bg-primary': description !== 'User' && description !== 'Organization', 'bg-secondary': description === 'User', 'bg-warning': description === 'Organization' }">
            <img :src="img" class="card-img-top rounded-circle bg-white" alt="...">
        </div>
        <div class="card-body">
            <h5 class="card-title">{{ name }}</h5>
            <p class="card-text" v-if="description !== null">{{ description.slice(0, 50) }}</p>
            <h5 v-if="description !== 'User' && description !== 'Organization'"><i
                    class="fa-solid fa-star text-warning"></i> {{ star }}</h5>
            <a :href="link" class="btn btn-outline-primary">Vedi su GitHub</a>
        </div>
    </div>
    <!-- Fine singolo elemento -->
</template>