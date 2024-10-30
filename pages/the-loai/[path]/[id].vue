<script setup>
import { useRoute } from 'vue-router'
import ModuleLayout from '@/components/module/ModuleLayout.vue';
import ProductList from '@/components/Category/ProductList.vue';
import PostList from '@/components/Category/PostList.vue';
import TheBreadcrumb from '@/components/Breadcrumb/TheBreadcrumb.vue';

const route = useRoute()
const apiURL = import.meta.env.VITE_API_URL;
const data = await $fetch(`${apiURL}/${route.params.path}-ca${route.params.id}`)

useSeoMeta({
  title: data.category.category_title,
  ogTitle: data.category.category_title,
  description: data.category.category_title,
  ogDescription: data.category.category_title,
})
</script>

<template>
  <div>
    <TheBreadcrumb :data="data.categories" :currentName="data.category.category_title" />
    <ModuleLayout :modules="data.modules" />
    <ProductList :categories="data" v-if="data.type === 1" />
    <PostList :categories="data" v-if="data.type === 2" />
  </div>
</template>

<style scoped></style>
