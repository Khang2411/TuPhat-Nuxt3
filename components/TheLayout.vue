<script setup>
import TheHeader from './header/TheHeader.vue';
import TheFooter from './footer/TheFooter.vue';

const apiURL = import.meta.env.VITE_API_URL;
const dataConfig = await $fetch(`${apiURL}/config`)
const dataMenu = await $fetch(`${apiURL}/menu`)

useHead({
  htmlAttrs: {
    lang: 'vi',
  },
})

useSeoMeta({
  title: dataConfig.seo_title,
  ogTitle: dataConfig.seo_title,
  description: dataConfig.seo_description,
  ogDescription: dataConfig.seo_description,
  ogImage: dataConfig.logo_header,
  twitterCard: 'summary_large_image',
})

onBeforeMount(() => {
  const installFacebookSdkScript = (d, s, id) => {
    let fjs = d.getElementsByTagName(s)[0]
    let js = d.createElement(s)
    js.id = id
    js.src = 'https://connect.facebook.net/vi_VN/sdk.js#xfbml=1&version=v21.0&appId=1438807890055526'
    js.async = true
    js.defer = true
    js.crossorigin='anonymous'
    fjs.parentNode.insertBefore(js, fjs)
  }
  installFacebookSdkScript(document, 'script', 'facebook-jssdk')
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
