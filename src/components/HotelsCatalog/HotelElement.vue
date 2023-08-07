<template>
  <div class="hotel-element">
    <div class="hotel-element__left">
      <div class="hotel-element__name">{{ props.injectedData.name }}</div>
      <div class="hotel-element__features">
        <div class="hotel-element__features-stars">
          <StarIcon
            :active="index < props.injectedData.stars"
            v-for="(star, index) in 5"
          />
        </div>
        <span class="hotel-element__features-type"> {{ props.injectedData.type }} </span>
        <div class="hotel-element__features-separator"></div>
        <span class="hotel-element__features-reviews">
          {{ props.injectedData.reviews_amount }} отзыва
        </span>
        <div class="hotel-element__features-location">
          <LocationIcon />
          <span>{{ props.injectedData.country }}</span>
        </div>
      </div>
      <p class="hotel-element__description">{{ props.injectedData.description }}</p>
    </div>
    <div class="hotel-element__right">
      <div class="hotel-element__price">
        <span class="hotel-element__price-number">{{ formattedPrice }}</span>
        <span class="hotel-element__price-label"> Цена за 1 ночь </span>
      </div>
      <SimpleButton size="sm" :type="btnType" @click.native="bookHotel">
        <OkIcon v-show="booked" /><ScheduleIcon v-show="!booked" /> {{ btnText }}
      </SimpleButton>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import StarIcon from "@/components/Icons/StarIcon.vue";
import LocationIcon from "@/components/Icons/LocationIcon.vue";
import OkIcon from "@/components/Icons/OkIcon.vue";
import ScheduleIcon from "@/components/Icons/ScheduleIcon.vue";
import SimpleButton from "../Buttons/SimpleButton.vue";

const props = defineProps({
  injectedData: {
    type: Object,
    default: [],
  },
});

const formattedPrice = computed(() => {
  const formatter = new Intl.NumberFormat("ru-RU", {
    minimumIntegerDigits: 1,
    maximumFractionDigits: 0,
    minimumFractionDigits: 0,
    style: "currency",
    currency: "RUB",
  });
  return formatter.format(props.injectedData.min_price);
});

const booked = ref(false);
const btnType = computed(() => (booked.value ? "opaque-green" : "opaque-purple"));
const btnText = computed(() => (booked.value ? "Забронировано" : "Забронировать"));

const bookHotel = () => {
  booked.value = !booked.value;
};
</script>

<style scoped lang="scss">
.hotel-element {
  padding: 25px;
  border: 1px solid $color_light-gray;
  border-radius: 20px;
  display: grid;
  grid-template-columns: 1fr 180px;
  gap: 46px;
  &__left {
    display: flex;
    flex-direction: column;
  }
  &__name {
    color: $color_black;
    margin-bottom: 8px;
    font-weight: 700;
    font-size: 20px;
  }
  &__features {
    display: flex;
    align-items: center;
    margin-bottom: 16px;
    &-stars {
      display: flex;
      align-items: center;
      gap: 6px;
      margin-right: 15px;
    }
    &-type {
      display: block;
      color: $color_dark-gray;
    }
    &-separator {
      width: 4px;
      height: 4px;
      border-radius: 50%;
      background: $color_gray;
      margin: 0 6px;
    }
    &-reviews {
      color: $color_dark-gray;
    }
    &-location {
      display: flex;
      gap: 8px;
      align-items: center;
      margin-left: 15px;
    }
  }
  &__right {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
  &__price {
    display: flex;
    flex-direction: column;
    &-number {
      text-align: end;
      font-size: 25px;
      font-weight: 700;
    }
    &-label {
      text-align: end;
    }
  }
}
</style>
