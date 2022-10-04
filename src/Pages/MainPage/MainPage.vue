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
    <DocsList
      :docsList.sync="docsList"
      :footerList.sync="footerList"
      :searchValue="searchValue"
      @onEdit="onEdit"
      @onDelete="onDelete"
      @onOpen="onOpen"
    />
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
    searchValue: '',
    footerList: [
      {
        id: 1,
        title: 'Тестовое задание кандидата',
      },
      {
        id: 2,
        title: 'Трудовой договор',
      },
      {
        id: 3,
        title: 'Мед. книжка',
      },
    ],
    docsList: [
      {
        id: 1,
        title: 'Обязательные для всех',
        isOpen: false,
        items: [
          {
            id: 1,
            title: 'Паспорт',
          },
          {
            id: 2,
            title: 'ИНН',
          }
        ]
      },
      {
        id: 2,
        title: 'Обязательные для трудоустройства',
        isOpen: false,
        items: [
          {
            id: 4,
            title: 'Свидетельство об оброзовании',
          }
        ]
      },
      {
        id: 3,
        title: 'Специальные',
        isOpen: false,
        items: [
          {
            id: 4,
            title: 'Регистрация ИП',
          },
        ]
      }
    ]
  }),
  methods: {
    onAddNewType (type) {
      this.docsList.push(type)
    },
    onAddNewDoc (newDoc) {
      this.footerList.push(newDoc)
    },
    onSearch (value) {
      this.searchValue = value
    },
    search (items) {
      const newArray = items.map((el) => {
        const { title } = el
        const newTitle = title.toLowerCase()
        return {
          ...el,
          isSearch: newTitle.search(this.searchValue.toLowerCase()) !== -1
        }
      })
      return newArray
    },
    onEdit ({ id }) {
      const currentItem = this.docsList.find((el) => el.id === id)
      currentItem.title = new Date()
    },
    onDelete ({ id }) {
      const currentIndex = this.docsList.findIndex((el) => el.id === id)
      this.docsList.splice(currentIndex, 1)
    },
    onOpen ({ id }) {
      const currentItem = this.docsList.find((el) => el.id === id)
      const { isOpen } = currentItem
      currentItem.isOpen = !isOpen
    }
  },
  watch: {
    searchValue () {
      this.footerList = this.search(this.footerList)
      this.docsList = this.search(this.docsList)
      this.docsList.forEach((el) => {
        const { items = [] } = el
        el.items = this.search(items)
      })
    }
  }
}

</script>

<style lang="scss" scoped>
@import "../../sass/variables";

  .main-page {
    margin: 20px 20px;
    display: grid;
    grid-gap: 20px 0;
  }
</style>