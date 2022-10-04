<template>
  <div
    class="docs-list-type-header"
    :class="[isBorderBottom && 'docs-list-type-header_border-bottom']"
  >
    <div
      class="docs-list-type-header__arrow"
      :class="[isOpen && 'docs-list-type-header__arrow_revert']"
      @click="onOpen"
    >
      <ArrowIcon/>
    </div>
    <div class="docs-list-type-header__title">
      {{ title }}
    </div>
    <ToolbarMenu
      :item="doc"
      @onEdit="onEdit"
      @onDelete="onDelete"
    />
  </div>
</template>

<script>
import {ArrowIcon} from "@/constants/icons";
import ToolbarMenu from "@/common/ToolbarMenu/ToolbarMenu";

export default {
  name: "DocsListTypeHeader",
  components: {
    ToolbarMenu,
    ArrowIcon,
  },
  props: {
    doc: {
      type: Object,
      default: () => ({})
    }
  },
  computed: {
    title () {
      const { title } = this.doc
      return title
    },
    isBorderBottom () {
      const { isOpen = false, items = [] } = this.doc
      return isOpen && items.length
    },
    isOpen () {
      const { isOpen = false } = this.doc
      return isOpen
    }
  },
  methods: {
    onEdit (doc) {
      this.$emit('onEdit', doc)
    },
    onDelete (doc) {
      this.$emit('onDelete', doc)
    },
    onOpen () {
      this.$emit('onOpen', this.doc)
    }
  }
}
</script>

<style scoped lang="scss">
@import "../../../../sass/variables";

  .docs-list-type-header {
    display: grid;
    grid-template-columns: 22px 1fr max-content;
    align-items: center;
    grid-gap: 0 14px;
    padding: 13px 16px 13px 16px;
    border-left: 1px solid $color-botticelli;
    border-right: 1px solid $color-botticelli;

    &_border-bottom {
      border-bottom: 1px solid $color-botticelli;
    }

    &__arrow {
      display: flex;
      color: $color-blue;
      cursor: pointer;
      transition: 0.2s;

      &_revert {
        transform: rotate(-180deg);
      }

      &:hover {
        opacity: 0.8;
      }
    }

    &__title {
      font-size: 15px;
      line-height: 16px;
      font-weight: 600;
    }
  }
</style>