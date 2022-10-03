<template>
  <div class="main-page">
    <MainHeader/>
    <SearchInput/>
    <DocsList/>
  </div>
</template>

<script>
import MainHeader from "@/components/MainHeader/MainHeader";
import SearchInput from "@/common/SearchInput/SearchInput";
import DocsList from "@/components/DocsList/DocsList";

export default {
  name: "MainPage",
  components: {
    DocsList,
    SearchInput,
    MainHeader
  }
}

</script>

<style lang="scss" scoped>

  .main-page {
    margin: 20px 20px;
  }
</style>