<template>
  <div
    class="docs-list-type"
    :class="[isBorderBottom && 'docs-list-type_last']"
  >
    <DocsListTypeHeader
      :doc="doc"
      @onEdit="onEdit"
      @onDelete="onDelete"
      @onOpen="onOpen"
    />
    <draggable
      :list="doc.items"
      v-bind="dragOptions()"
      group="type-item"
      class="docs-list-type__wrap"
      :style="typeStyle"
    >
      <template v-for="item in doc.items">
       <DocsListTypeItem
         v-if="searchValue ? item.isSearch: true"
         :item="item"
         :key="item.id"
         :style="{height: `${doc.isOpen ? heightItem : 0}px`}"
         @onEdit="onEditItem"
         @onDelete="onDeleteItem"
       />
      </template>
    </draggable>
  </div>
</template>

<script>
import draggable from 'vuedraggable'
import DocsListTypeItem from "@/components/DocsList/DocsListType/DocsListTypeItem/DocsListTypeItem";
import DocsListTypeHeader from "@/components/DocsList/DocsListType/DocsListTypeHeader/DocsListTypeHeader";

export default {
  name: "DocsListType",
  components: {
    DocsListTypeHeader,
    DocsListTypeItem,
    draggable
  },
  props: {
    doc: {
      type: Object,
      default: () => ({})
    },
    searchValue: {
      type: String,
      default: ''
    }
  },
  data: () => ({
    heightItem: 35
  }),
  computed: {
    isBorderBottom () {
      const { isOpen = false, items = [] } = this.doc
      return isOpen && items.length
    },
    typeStyle () {
      const { isOpen = false, items = [] } = this.doc
      const height = this.searchValue ? items.filter((el) => el.isSearch) : items
      return {
        height: `${isOpen ? height.length * this.heightItem : 0}px`,
        zIndex: isOpen ? 1 : -1,
        opacity: isOpen ? 1 : 0,
      }
    },
  },
  methods: {
    dragOptions () {
      return {
        handle: '.toolbar-menu__icon_drop',
        animation: 200,
        disabled: false
      }
    },
    onEdit (doc) {
      this.$emit('onEdit', doc)
    },
    onDelete (doc) {
      this.$emit('onDelete', doc)
    },
    onOpen (doc) {
      this.$emit('onOpen', doc)
    },
    onEditItem ({ id }) {
      const { items = [] } = this.doc
      const currentItem = items.find((el) => el.id === id)
      currentItem.title = new Date()
    },
    onDeleteItem ({ id }) {
      const { items = [] } = this.doc
      const currentIndex = items.find((el) => el.id === id)
      items.splice(currentIndex, 1)
      if (!items.length) this.onOpen(this.doc)
    },
  }
}
</script>

<style scoped lang="scss">
  @import "../../../sass/variables";

  .docs-list-type {
    border-bottom: 1px solid $color-botticelli;

    &:first-child {
      border-top: 1px solid $color-botticelli;
    }

    &_last {
      &:nth-last-child(-n+2) {
        border-bottom: 0;

        .docs-list-type__wrap {
          border-bottom: 1px solid $color-botticelli;
        }
      }
    }

    &__wrap {
      margin: 0 0 0 16px;
      position: relative;
      transition: all 0.2s;
    }
  }
</style>