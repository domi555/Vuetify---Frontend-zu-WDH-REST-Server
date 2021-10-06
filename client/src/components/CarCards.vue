<template>
  <v-main>
    <div class="d-flex flex-wrap justify-center mt-4">
      <CarCard
        v-for="(car, i) in cars"
        :key="i"
        :car="car"
        class="ma-3"
        @reserve="reserve"
      ></CarCard>
    </div>
  </v-main>
</template>

<script>
import CarCard from './CarCard.vue';
import axios from 'axios';

export default {
  components: {
    CarCard,
  },
  props: {
    cars: {
      type: Array,
    },
  },
  methods: {
    async reserve(car) {
      try {
        await axios({
          url: `http://localhost:3000/cars/${car.id}`,
          method: 'patch',
          contentType: 'application/json',
          data: {
            title: `${car.title} RESERVED`,
          },
        });
        this.$emit('refresh');
      } catch {
        console.error('Error');
      }
    },
  },
};
</script>
