<template>
  <div class="app">
    <MainHeader/>
    <SearchInput/>
    <DocsList/>
  </div>
</template>

<script>

import SearchInput from "@/common/SearchInput/SearchInput";
import MainHeader from "@/components/MainHeader/MainHeader";
import DocsList from "@/components/DocsList/DocsList";

export default {
  name: 'App',
  components: {
    DocsList,
    MainHeader,
    SearchInput
  }
}
</script>

<style>

</style>