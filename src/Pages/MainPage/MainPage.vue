<template>
  <div class="main-page">
    <MainHeader
      @onAddNewType="onAddNewType"
      @onAddNewDoc="onAddNewDoc"
    />
    <SearchInput
      :searchValue="searchValue"
      placeholder="Поиск"
      @onSearch="onSearch"
    />
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
  },
  data: () => ({
    searchValue: ''
  }),
  methods: {
    onAddNewType () {
    },
    onAddNewDoc () {
    },
    onSearch (value) {
      this.searchValue = value
    }
  }
}

</script>

<style lang="scss" scoped>

  .main-page {
    margin: 20px 20px;
    display: grid;
    grid-gap: 20px 0;
  }
</style>