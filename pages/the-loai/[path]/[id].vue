<script setup>
import { useRoute } from 'vue-router'
import ModuleLayout from '@/components/module/ModuleLayout.vue';
import ProductList from '@/components/Category/ProductList.vue';
import PostList from '@/components/Category/PostList.vue';
import TheBreadcrumb from '@/components/Breadcrumb/TheBreadcrumb.vue';

const route = useRoute()
const apiURL = import.meta.env.VITE_API_URL;
const data = await $fetch(`${apiURL}/${route.params.path}-ca${route.params.id}?page=${route.query.page}`)
const dataCate = ref(data)

useSeoMeta({
  title: data.category.category_title,
  ogTitle: data.category.category_title,
  description: data.category.category_title,
  ogDescription: data.category.category_title,
})

watch(route, async (current) => {
  dataCate.value = await $fetch(`${apiURL}/${current.params.path}-ca${current.params.id}?page=${current.query.page}`, {
    async onRequest() {
      document.getElementById("ht-preloader").style.display = "flex";
    },
    async onResponse({ request, response }) {
      console.log("[fetch response]", request, response.status, response.body);
      document.getElementById("ht-preloader").style.display = "none";
    },
  })
  window.scrollTo({ top: 700 });
})
</script>

<template>
  <div>
    <TheBreadcrumb :data="dataCate.categories" :currentName="dataCate.category.category_title" />
    <ModuleLayout :modules="dataCate.modules" />
    <ProductList :categories="dataCate" v-if="dataCate.type === 1" />
    <PostList :categories="dataCate" v-if="dataCate.type === 2" />
  </div>
</template>

<style scoped></style>
