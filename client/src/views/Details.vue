<template>
  <div class="d-flex flex-wrap justify-center mt-4">
    <v-card max-width="500">
      <v-img height="250" :src="car.image"></v-img>
      <v-card-title>{{
        `${car.title} ${car.status == 'reserved' ? '*RESERVED*' : ''}`
      }}</v-card-title>
      <v-card-text>
        <v-simple-table>
          <thead>
            <tr>
              <th class="text-left">
                Price
              </th>
              <th class="text-left">
                Miles
              </th>
              <th class="text-left">
                Year Of Make
              </th>
              <th class="text-left">
                Current Owner
              </th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>
                {{ car.status != 'reserved' ? price : 'N/A' }}
              </td>
              <td>{{ car.miles }}</td>
              <td>{{ car.year_of_make }}</td>
              <td>{{ `${car.first_name} ${car.last_name}` }}</td>
            </tr>
          </tbody>
        </v-simple-table>
        <div class="mb-3">
          {{ car.description }}
        </div>
      </v-card-text>
      <v-card-actions class="ma-2">
        <v-btn class="purple darken-3 white--text" :to="`/`">Go Back</v-btn>
        <v-spacer></v-spacer>
        <v-btn
          v-if="car.status != 'reserved'"
          class="red darken-3 white--text"
          @click="orderCar(car.id)"
          >Order Car</v-btn
        >
      </v-card-actions>
    </v-card>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Details',
  props: {
    cars: {
      type: Array,
    },
    id: {
      type: String,
    },
  },
  computed: {
    car() {
      return this.cars.find((el) => el.id == this.id);
    },
    price() {
      return `${new Intl.NumberFormat('en').format(Number(this.car.price))} $`;
    },
  },
  methods: {
    async orderCar(id) {
      try {
        await axios({
          url: `http://localhost:3000/cars/${id}`,
          method: 'patch',
          data: {
            status: 'reserved',
          },
        });
        this.$emit('reload');
      } catch {
        console.error('Error');
      }
    },
  },
};
</script>
