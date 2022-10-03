<template>
  <div
    class="custom-button"
    @click="onButtonClick"
  >
    <div class="custom-button__icon">
      <PlusIcon/>
    </div>
    <div class="custom-button__text">
      {{ title }}
    </div>
  </div>
</template>

<script>
import {PlusIcon} from "@/constants/icons";

export default {
  name: "CustomButton",
  components: {
    PlusIcon
  },
  props: {
    title: {
      type: String,
      default: ''
    }
  },
  methods: {
    onButtonClick () {
      this.$emit('onButtonClick')
    }
  }
}
</script>


<style scoped lang="scss">
  @import "../../sass/variables";

  .custom-button {
    display: flex;
    align-items: center;
    justify-content: center;
    grid-gap: 0 10px;
    padding: 5px 10px 5px 10px;
    border: 1px solid $color-mischka;
    border-radius: 50px;
    cursor: pointer;
    transition: 0.15s;

    &__icon {
      display: flex;
      color: $color-blue
    }

    &__text {
      font-size: 12px;
      line-height: 13px;
      font-weight: 500;
    }

    &:hover {
      opacity: 0.8;
    }
  }

</style>