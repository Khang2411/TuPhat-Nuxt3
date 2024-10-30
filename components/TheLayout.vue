<script setup>
import TheHeader from './header/TheHeader.vue';
import TheFooter from './footer/TheFooter.vue';
const apiURL = import.meta.env.VITE_API_URL;
const dataConfig = await $fetch(`${apiURL}/config`)
const dataMenu = await $fetch(`${apiURL}/menu`)

useSeoMeta({
  title: dataConfig.seo_title,
  ogTitle: dataConfig.seo_title,
  description: dataConfig.seo_description,
  ogDescription: dataConfig.seo_description,
  ogImage: dataConfig.logo_header,
  twitterCard: 'summary_large_image',
})
</script>

<template>
  <div>
    <TheHeader :data="dataConfig" :dataMenu="dataMenu" />
    <slot></slot>
    <TheFooter :logo="dataConfig.logo_footer" :logoSocial="dataConfig.social" />
  </div>
</template>

<style scoped></style>
