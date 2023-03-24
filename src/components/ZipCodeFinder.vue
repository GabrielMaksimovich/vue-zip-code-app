<template>
  <div className="zip-code-finder">
    <input className="zip-code-finder__input" v-model="zipCode" placeholder="Enter ZIP code">
    <button className="zip-code-finder__button" @click="search">Search</button>
    <div v-if="address" className="zip-code-finder__address">
      <p>{{ address.places[0]['place name'] }}</p>
      <p>{{ address.places[0].state }}</p>
    </div>
    <div v-if="errorMessage" className="zip-code-finder__error">
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

<style>
.zip-code-finder {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.zip-code-finder__input {
  margin-bottom: 10px;
  padding: 5px;
  border: none;
  border-bottom: 1px solid #ccc;
}

.zip-code-finder__button {
  background-color: #007bff;
  color: white;
  padding: 5px 10px;
  border: none;
  border-radius: 3px;
}

.zip-code-finder__address {
  margin-top: 10px;
}

.zip-code-finder__error {
  color: red;
  margin-top: 10px;
}
</style>
