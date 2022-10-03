<template>
  <div class="main-header">
    <div class="main-header__title">
      Документы
    </div>
    <BookmarksIcon/>
    <CustomButton
      title="Новый тип"
      @onButtonClick="onAddNewType"
    />
    <CustomButton
      title="Новый документ"
      @onButtonClick="onAddNewDoc"
    />
  </div>
</template>

<script>
import {BookmarksIcon} from "@/constants/icons";
import CustomButton from "@/common/CustomButton/CustomButton";

export default {
  name: "MainHeader",
  components: {
    CustomButton,
    BookmarksIcon
  },
  data: () => ({
  }),
  methods: {
    onAddNewType () {
      this.$emit('onAddNewType')
    },
    onAddNewDoc () {
      this.$emit('onAddNewDoc')
    }
  }
}
</script>

<style scoped lang="scss">
@import "../../sass/variables";

 .main-header {
  display: grid;
   grid-template-columns: 1fr 30px 115px 150px;
   grid-gap: 0 10px;

   &__title {
     font-size: 22px;
     line-height: 24px;
     font-weight: 500;
     color: $color-black
   }

 }

</style>