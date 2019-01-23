<template>
  <div id="errorWrapper">
    <h1 v-if="error.statusCode === 404">Page not found {{error.statusCode}}</h1>
    <h1 v-else>An error occurred {{error.statusCode}}</h1>
    <nuxt-link to="/">사이트로 돌아가기</nuxt-link>
  </div>
</template>

<script>
export default {
  props: ['error'],
  layout: 'errorLayout'
}
</script>

<style>
  #errorWrapper {
    font-size: 18px;
    text-align: center;
  }
</style>