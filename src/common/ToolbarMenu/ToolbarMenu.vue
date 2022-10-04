<template>
  <div class="toolbar-menu">
    <div
      v-for="icon in icons"
      :key="icon.key"
      :class="[
        'toolbar-menu__icon',
        `toolbar-menu__icon_${icon.key}`
      ]"
      @click="onClick(icon)"
    >
      <component :is="icon.icon" />
    </div>
  </div>
</template>

<script>
import {DeleteIcon, DropArrowIcon, PencilIcon} from "@/constants/icons";

export default {
  name: "ToolbarMenu",
  props: {
    item: {
      type: Object,
      default: () => ({})
    }
  },
  data: () => ({
    icons: [
      {
        key: 'pencil',
        icon: PencilIcon,
        funcName: 'onEdit'
      },
      {
        key: 'delete',
        icon: DeleteIcon,
        funcName: 'onDelete'
      },
      {
        key: 'drop',
        icon: DropArrowIcon,
        funcName: ''
      },
    ]
  }),
  methods: {
    onClick ({ funcName }) {
      if (funcName) this[funcName]()
    },
    onEdit () {
      this.$emit('onEdit', this.item)
    },
    onDelete () {
      this.$emit('onDelete', this.item)
    }
  }
}
</script>

<style scoped lang="scss">
  @import "../../sass/variables";

  .toolbar-menu {
    display: flex;
    align-items: center;
    grid-gap: 0 14px;

    &__icon {
      display: flex;
      justify-content: center;
      align-items: center;
      width: 20px;
      height: 20px;
      cursor: pointer;
      transition: 0.2s;

      &_pencil {
        color: $color-nepal;
      }

      &_delete {
        color: $color-persian-rose;
      }

      &_drop {
        color: $color-nepal;
      }

      &:hover {
        opacity: 0.8;
      }
    }
  }
</style>