<template>
  <v-app>
    <LogoBar></LogoBar>
    <v-main>
      <router-view :cars="cars" @reload="loadCars" />
    </v-main>
  </v-app>
</template>

<script>
import LogoBar from '@/components/LogoBar.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    LogoBar,
  },
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
