<script setup>
import TheHeader from './header/TheHeader.vue';
import TheFooter from './footer/TheFooter.vue';

const apiURL = import.meta.env.VITE_API_URL;
const dataConfig = await $fetch(`${apiURL}/config`)
const dataMenu = await $fetch(`${apiURL}/menu`)

useSeoMeta({
  htmlAttrs: {
    lang: "vi",
  },
  title: dataConfig.seo_title,
  ogTitle: dataConfig.seo_title,
  description: dataConfig.seo_description,
  ogDescription: dataConfig.seo_description,
  ogImage: dataConfig.logo_header,
  twitterCard: 'summary_large_image',
})

onMounted(() => {
  const installFacebookSdkScript = (d, s, id) => {
    let fjs = d.getElementsByTagName(s)[0]
    let js = d.createElement(s)
    js.id = id
    js.src = 'https://connect.facebook.net/en_US/sdk.js'
    fjs.parentNode.insertBefore(js, fjs)
  }
  installFacebookSdkScript(document, 'script', 'facebook-jssdk')

  window.fbAsyncInit = () => {
    FB.init({
      appId: '1438807890055526',
      cookie: true,
      xfbml: true,
      version: 'v3.2'
    })

    FB.AppEvents.logPageView()
  }
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
