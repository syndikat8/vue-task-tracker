<template>
  <div class="docs-list-type">
    <DocsListTypeHeader
      :doc="doc"
      @onEdit="onEdit"
      @onDelete="onDelete"
      @onOpen="onOpen"
    />
    <draggable
      v-if="doc.isOpen"
      :list="doc.items"
      v-bind="dragOptions()"
      group="type-item"
      class="docs-list-type__wrap"
    >
     <DocsListTypeItem
       v-for="item in doc.items"
       :item="item"
       :key="item.id"
       @onEdit="onEditItem"
       @onDelete="onDeleteItem"
     />
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
    }
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

    &__wrap {
      margin: 0 0 0 16px;
    }
  }
</style>