<template>
  <div class="docs-list">
    <draggable
      :list="docs"
      v-bind="dragOptions()"
    >
     <DocsListType
       v-for="doc in docs"
       :doc="doc"
       :key="doc.id"
       @onEdit="onEdit"
       @onDelete="onDelete"
       @onOpen="onOpen"
     />
      <div class="docs-list__footer">
       <draggable
        :list="footerElements"
        group="type-item"
        v-bind="dragOptions()"
       >
         <DocsListTypeItem
           v-for="item in footerElements"
           :item="item"
           :key="item.id"
           :isFooter="true"
           @onEdit="onEditItem"
           @onDelete="onDeleteItem"
         />
       </draggable>
      </div>
    </draggable>
  </div>
</template>

<script>
import draggable from 'vuedraggable'
import DocsListType from "@/components/DocsList/DocsListType/DocsListType";
import DocsListTypeItem from "@/components/DocsList/DocsListType/DocsListTypeItem/DocsListTypeItem";

export default {
  name: "DocsList",
  components: {
    DocsListTypeItem,
    DocsListType,
    draggable
  },
  props: {
    docsList: {
      type: Array,
      default: () => ([])
    },
    footerList: {
      type: Array,
      default: () => ([])
    }
  },
  computed: {
    docs: {
      get () {
        return this.docsList
      },
      set (data) {
        this.$emit('update:docsList', data)
      }
    },
    footerElements: {
      get () {
        return this.footerList
      },
      set (data) {
        this.$emit('update:footerList', data)
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
      const currentItem = this.footerElements.find((el) => el.id === id)
      currentItem.title = new Date()
    },
    onDeleteItem ({ id }) {
      const currentIndex = this.footerElements.find((el) => el.id === id)
      this.footerElements.splice(currentIndex, 1)
    },
  }
}
</script>

<style scoped lang="scss">
@import "../../sass/variables";

  .docs-list {

    &__footer {
      margin: 20px 0 0 0;
      //border-top: 1px solid $color-botticelli;
      //border-bottom: 1px solid $color-botticelli;
    }
  }
</style>