<script setup>
defineProps({
    links: Object,
})
</script>

<template>
    <nav aria-label="..." class="mt-5">
        <ul class="pagination justify-content-center">
            <li class="page-item">
                <a class="page-link text-dark" href="#">Trước</a>
            </li>

            <li class="page-item" v-for="(paginate, index) in links" :key="index">
                <RouterLink :to="{ query: { page: Number(paginate.label) ? paginate.label : 1 } }" class="page-link"
                    :class="($route.query.page ? $route.query.page : '1') === paginate.label ? 'page-current-active text-white' : 'text-dark'">
                    {{ paginate.label }}
                </RouterLink>
            </li>

            <li class="page-item">
                <a class="page-link text-dark" href="#">Sau</a>
            </li>
        </ul>
    </nav>
</template>

<style scoped>
.page-current-active {
    background-color: #003789;
}
</style>
