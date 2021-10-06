<template>
  <v-card max-width="300" class="flex d-flex flex-column">
    <div>
      <v-img height="250" :src="car.image"></v-img>
    </div>
    <v-card-title>{{
      `${car.title} ${car.status == 'reserved' ? '*RESERVED*' : ''}`
    }}</v-card-title>
    <v-card-text class="flex">
      <div class="mb-2">
        Owner:
        <span class="font-weight-bold">{{
          `${car.first_name} ${car.last_name}`
        }}</span>
      </div>
      <div>
        Year: <span class="font-weight-bold">{{ car.year_of_make }}</span>
      </div>
      <div class="mb-2">
        Miles: <span class="font-weight-bold">{{ car.miles }}</span>
      </div>
      <div class="mb-3">
        Price:
        <span class="font-weight-bold">{{
          car.status != 'reserved' ? car.price : 'N/A'
        }}</span>
      </div>
    </v-card-text>
    <v-card-actions class="ma-2">
      <v-spacer></v-spacer>
      <v-btn
        v-if="car.status != 'reserved'"
        class="purple darken-3 white--text"
        :to="`/details/${car.id}`"
        >Details</v-btn
      >
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  props: {
    car: {
      type: Object,
    },
  },
};
</script>
