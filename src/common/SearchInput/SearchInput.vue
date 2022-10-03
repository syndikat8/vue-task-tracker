<template>
  <div class="search-input">
    <div class="search-input__search">
      <SearchIcon/>
    </div>
    <input
      class="search-input__input"
      :value="searchValue"
      :placeholder="placeholder"
      @input="onSearch($event)"
    />
    <transition name="fade">
      <div
        v-if="searchValue"
        class="search-input__cross"
        @click="onReset"
      >
        <CrossIcon/>
      </div>
    </transition>
  </div>
</template>

<script>
import {SearchIcon, CrossIcon} from "@/constants/icons";

export default {
  name: 'SearchInput',
  components: {
    SearchIcon,
    CrossIcon
  },
  props: {
    searchValue: {
      type: String,
      default: ''
    },
    placeholder: {
      type: String,
      default: ''
    }
  },
  methods: {
    onSearch ({ target }) {
      const { value } = target
      this.$emit('onSearch', value.trim())
    },
    onReset () {
      this.$emit('onSearch', '')
    }
  }
}

</script>

<style scoped lang="scss">
  @import "../../sass/variables";

  .search-input {
    display: flex;
    align-items: center;
    position: relative;
    width: 560px;

    &__input {
      width: 100%;
      padding: 12px 30px 12px 30px;
      font-size: 15px;
      line-height: 16px;
      font-weight: 400;
      border: none;
      border-bottom: 1px solid $color-nepal;
      transition: 0.2s;

      &::-webkit-input-placeholder {
        color: $color-nepal;
        font-style: italic;
      }

      &:focus {
        border-bottom-color: $color-blue;
      }
    }

    &__search {
      position: absolute;
    }

    &__cross {
      position: absolute;
      right: 0;
      color: $color-persian-rose;
      cursor: pointer;
      transition: 0.2s;

      &:hover {
        opacity: 0.8;
      }
    }
  }

</style>