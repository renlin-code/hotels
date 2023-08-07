<template>
  <div class="no-results">
    <NoResultsFigure class="no-results__figure" />
    <h6 class="no-results__title">По данным параметрам ничего не найдено</h6>
    <p class="no-results__text">
      Попробуйте изменить параметры фильтрации или вернуться в общий каталог
    </p>
    <div class="no-results__btn-wrapper">
      <SimpleButton size="md" type="opaque-purple" @click.native="emits('action-btn')"
        >Очистить фильтр</SimpleButton
      >
    </div>
  </div>
</template>

<script setup>
import NoResultsFigure from "@/components/Figures/NoResultsFigure.vue";
import SimpleButton from "../Buttons/SimpleButton.vue";

const emits = defineEmits(["action-btn"]);
</script>

<style scoped lang="scss">
.no-results {
  width: 390px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  &__figure {
    margin-bottom: 34px;
  }
  &__title {
    font-size: 18px;
    font-weight: 700;
    margin-bottom: 8px;
    text-align: center;
  }
  &__text {
    color: $color_gray;
    margin-bottom: 23px;
    text-align: center;
  }
  &__btn-wrapper {
    margin: 0 auto;
    width: 240px;
  }
}
</style>
