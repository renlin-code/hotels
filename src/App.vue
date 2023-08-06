<template>
  <header></header>

  <main v-if="hotels">
    <section class="hotels-catalog container">
      <div class="hotels-catalog__left">
        <div class="hotels-catalog__filters filters">
          <div class="filters__group">
            <div class="filters__group-name">Страна</div>
            <FilterSearch
              :items="allCountries"
              @setSelectedItems="setCountries"
              :resetTrigger="resetTrigger"
            />
          </div>
          <div class="filters__group">
            <div class="filters__group-name">Тип</div>
            <FilterCheckboxes
              :items="allTypes"
              @setSelectedItems="setTypes"
              :resetTrigger="resetTrigger"
            />
          </div>
          <div class="filters__group">
            <div class="filters__group-name">Количество звезд</div>
            <FilterCheckboxes
              :items="allStars"
              @setSelectedItems="setSelectedStars"
              :resetTrigger="resetTrigger"
            />
          </div>
          <div class="filters__group">
            <div class="filters__group-name">Количество отзывов (от)</div>
            <FilterInput
              placeholder="Например, от 10"
              @setInputValue="setMinAmountOfReviews"
              :resetTrigger="resetTrigger"
            />
          </div>
          <div class="filters__group">
            <div class="filters__group-name">Цена до</div>
            <FilterRange
              :minMaxRange="minMaxRange"
              @setSelectedRange="setSelectedRange"
              :resetTrigger="resetTrigger"
            />
          </div>
        </div>
        <div class="hotels-catalog__buttons buttons">
          <SimpleButton primary @click.native="applyFilters">
            Применить фильтр
          </SimpleButton>
          <SimpleButton @click.native="reset"> Очистить фильтр </SimpleButton>
        </div>
      </div>
      <div class="hotels-catalog__right">
        <ul class="hotels-catalog__hotels hotels">
          <li class="hotels__item" v-for="hotel in hotelsFiltered">
            <HotelElement :injected-data="hotel" />
          </li>
        </ul>
      </div>
    </section>
  </main>
</template>

<script setup>
import { ref, computed, nextTick } from "vue";

import FilterSearch from "@/components/Filters/FilterSearch.vue";
import FilterCheckboxes from "@/components/Filters/FilterCheckboxes.vue";
import FilterInput from "@/components/Filters/FilterInput.vue";
import FilterRange from "@/components/Filters/FilterRange.vue";
import HotelElement from "./components/HotelsCatalog/HotelElement.vue";
import SimpleButton from "./components/Buttons/SimpleButton.vue";

const hotels = ref(null);
const hotelsFiltered = ref(null);
(async () => {
  const res = await fetch("/placeholders/hotels.json");
  const data = await res.json();
  hotels.value = data.hotels;
  hotelsFiltered.value = hotels.value;
})();

const allCountries = computed(() => [...new Set(hotels.value?.map((i) => i.country))]);
const selectedCountries = ref(null);
const setCountries = (payload) => (selectedCountries.value = payload);

const allTypes = computed(() => [...new Set(hotels.value?.map((i) => i.type))]);
const selectedTypes = ref([]);
const setTypes = (payload) => (selectedTypes.value = payload);

const allStars = ["1", "2", "3", "4", "5"];
const selectedStars = ref([]);
const setSelectedStars = (payload) => (selectedStars.value = payload);

const minAmountOfReviews = ref(null);
const setMinAmountOfReviews = (payload) => (minAmountOfReviews.value = payload);

const minMaxRange = computed(() => {
  const allPrices = [...new Set(hotels.value?.map((i) => i.min_price))];
  const minPrice = Math.min(...allPrices);
  const maxPrice = Math.max(...allPrices);
  return [Math.floor(minPrice), Math.ceil(maxPrice)];
});
const selectedRange = ref([]);
const setSelectedRange = (payload) => (selectedRange.value = payload);

const applyFilters = () => {
  hotelsFiltered.value = hotels.value
    .filter((hotel) =>
      selectedCountries.value ? selectedCountries.value.includes(hotel.country) : true
    )
    .filter((hotel) =>
      selectedTypes.value.length > 0 ? selectedTypes.value.includes(hotel.type) : true
    )
    .filter((hotel) =>
      selectedStars.value.length > 0
        ? selectedStars.value.includes(`${hotel.stars}`)
        : true
    )
    .filter((hotel) =>
      minAmountOfReviews.value > 0
        ? hotel.reviews_amount >= minAmountOfReviews.value
        : true
    )
    .filter((hotel) =>
      selectedRange.value.length > 0
        ? hotel.min_price >= selectedRange.value[0] &&
          hotel.min_price <= selectedRange.value[1]
        : true
    );
};

const resetTrigger = ref(false);
const reset = async () => {
  resetTrigger.value = !resetTrigger.value;
  await nextTick();
  applyFilters();
};
</script>

<style scoped lang="scss">
.hotels-catalog {
  display: grid;
  grid-template-columns: 325px 1fr;
  gap: 40px;
  .hotels {
    display: flex;
    flex-direction: column;
    gap: 15px;
  }
  .filters {
    display: flex;
    flex-direction: column;
    gap: 25px;
    margin-bottom: 40px;
    &__group {
      &-name {
        margin-bottom: 14px;
      }
    }
  }
  .buttons {
    display: flex;
    flex-direction: column;
    gap: 15px;
  }
}
</style>
