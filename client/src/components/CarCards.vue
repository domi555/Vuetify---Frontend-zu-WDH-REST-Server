<template>
  <v-main>
    <div class="d-flex flex-wrap justify-center mt-4">
      <CarCard
        v-for="(car, i) in cars"
        :key="i"
        :car="car"
        class="ma-3"
      ></CarCard>
    </div>
  </v-main>
</template>

<script>
import CarCard from './CarCard.vue';

export default {
  components: {
    CarCard,
  },
  props: {
    cars: {
      type: Array,
    },
  },
};
</script>
