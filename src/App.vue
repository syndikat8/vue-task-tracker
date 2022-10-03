<template>
  <div class="app">
    <MainPage/>
  </div>
</template>

<script>

import MainPage from "@/Pages/MainPage/MainPage";

export default {
  name: 'App',
  components: {
    MainPage,
  }
}
</script>

<style lang="scss">
  @import "sass/style";
</style>