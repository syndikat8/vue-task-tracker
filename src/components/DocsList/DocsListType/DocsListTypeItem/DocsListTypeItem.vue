<template>
  <div
    class="docs-list-type-item"
    :class="[isFooter && 'docs-list-type-item_footer']"
  >
    <div class="docs-list-type-item__title">
      {{item.title}}
    </div>
    <ToolbarMenu
      :item="item"
      @onEdit="onEdit"
      @onDelete="onDelete"
    />
  </div>
</template>

<script>
import ToolbarMenu from "@/common/ToolbarMenu/ToolbarMenu";

export default {
  name: "DocsListTypeItem",
  components: {
    ToolbarMenu,
  },
  props: {
    item: {
      type: Object,
      default: () => ({})
    },
    isFooter: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    onEdit (doc) {
      this.$emit('onEdit', doc)
    },
    onDelete (doc) {
      this.$emit('onDelete', doc)
    }
  }
}
</script>

<style scoped lang="scss">
  @import "../../../../sass/variables";

  .docs-list-type-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 35px;
    padding: 9px 15px 9px 15px;
    border-left: 1px solid $color-botticelli;
    border-right: 1px solid $color-botticelli;
    transition: all 0.2s;

    & + & {
      border-top: 1px solid $color-botticelli;
    }

    &_footer {

      &:first-child {
        border-top: 1px solid $color-botticelli;
      }

      &:last-child {
        border-bottom: 1px solid $color-botticelli;
      }
    }

    &__title {
      font-size: 13px;
      line-height: 14px;
      font-weight: 400;
    }
  }
</style>