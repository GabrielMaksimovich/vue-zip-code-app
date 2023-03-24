<template>
  <div class="zip-code-finder">
    <form class="zip-code-finder__form">
      <input class="zip-code-finder__input" v-model="zipCode" placeholder="Enter ZIP code">
      <button type="button" class="zip-code-finder__button" @click="search">Search</button>
    </form>
    <div v-if="address" class="zip-code-finder__result">
      <p class="zip-code-finder__result-country">{{ address.country }}</p>
      <p class="zip-code-finder__result-city">{{ address.places[0]['place name'] }}</p>
      <p class="zip-code-finder__result-state">{{ address.places[0].state }}</p>
      <p class="zip-code-finder__result-other">long: {{ address.places[0].longitude }}</p>
      <p class="zip-code-finder__result-other">lat: {{ address.places[0].latitude }}</p>
    </div>
    <div v-if="errorMessage" class="zip-code-finder__error">

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
  async mounted() {
    // Capturing user agent
    const userAgent = navigator.userAgent;

    // Capturing utm get arguments from the current URL
    const urlParams = new URLSearchParams(window.location.search);

    const utmData = {};
    for (let [key, value] of urlParams.entries()) {
      if (key.startsWith('utm')) {
        utmData[key] = value;
      }
    }
    const response = await axios.get(`http://127.0.0.1:3000?format=json`,{
      headers: {
        "Target-URL": "https://api.ipify.org"
      }
    });

    const userIp = response.data.ip;
    console.log(response);
    console.log(`User agent: ${userAgent}`);
    console.log(`UTM data: `, utmData);
    console.log(`User IP: ${userIp}`);

  },
  methods: {
    async search() {
      try {
        const response = await axios.get(`http://127.0.0.1:3000/us/${this.zipCode}`,{
          headers: {
            "Target-URL": "https://api.zippopotam.us"
          }
        });
        this.address = response.data;
        this.errorMessage = '';
        console.log('try')
      } catch (error) {
        console.log(error);
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
}

.zip-code-finder__form {
  display: flex;
  justify-content: center;
  align-items: center;
}

.zip-code-finder__input {
  margin-right: 10px;
  padding: 5px;

  border-radius: 5px;
  outline: none;

  transition: transform 0.3s ease;
}

.zip-code-finder__input:hover {
  transform: scale(1.1);
}

.zip-code-finder__button {
  background-color: blue;
  color: white;
  padding: 5px;
  border-radius: 5px;
}

.zip-code-finder__result {
  margin-top: 10px;
}

.zip-code-finder__result-country {
  font-size: 18px;
  font-weight: bold;
}

.zip-code-finder__result-city {
  margin: 0;
  font-weight: bold;
}

.zip-code-finder__result-state {
  margin: 0;
}

.zip-code-finder__result-other {
  color: darkolivegreen;
}

.zip-code-finder__error {
  margin-top: 10px;
  color: red;
}
</style>
