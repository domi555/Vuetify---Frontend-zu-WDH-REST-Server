<template>
  <v-app>
    <v-main>
      <router-view :cars="cars" />
    </v-main>
  </v-app>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',
  data: () => ({
    cars: null,
  }),
  async created() {
    await this.loadCars();
  },
  methods: {
    async loadCars() {
      try {
        const result = await axios({
          url: 'http://localhost:3000/cars',
          method: 'get',
        });
        this.cars = result.data;
      } catch {
        console.error('Error');
      }
    },
  },
};
</script>
