<template>
  <div>
    <input v-model="zipCode" placeholder="Enter ZIP code">
    <button @click="search">Search</button>
    <div v-if="address">
      <p>{{ address.places[0]['place name'] }}</p>
      <p>{{ address.places[0].state }}</p>
    </div>
    <div v-if="errorMessage">
      {{ errorMessage }}
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      zipCode: '',
      address: null,
      errorMessage: ''
    };
  },
  methods: {
    async search() {
      try {
        const response = await axios.get(`https://api.zippopotam.us/us/${this.zipCode}`);
        this.address = response.data;
        this.errorMessage = '';
      } catch (error) {
        this.address = null;
        this.errorMessage = 'Invalid ZIP code';
      }
    }
  }
};
</script>
