<template>
  <div class="zip-code-finder">
    <form class="zip-code-finder__form" @submit.prevent="search">
      <input class="zip-code-finder__input" v-model="zipCode" placeholder="Enter ZIP code">
      <button type="submit" class="zip-code-finder__button">
        <svg stroke="currentColor" fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round" color="#FFF" height="25" width="25" xmlns="http://www.w3.org/2000/svg" style="color: rgb(255, 255, 255);">
          <circle cx="11" cy="11" r="8"></circle>
          <line x1="21" y1="21" x2="16.65" y2="16.65"></line>
        </svg>
      </button>
    </form>
    <div v-if="address" class="zip-code-finder__result">
      <p class="zip-code-finder__result-country">{{ address.country }}</p>
      <p class="zip-code-finder__result-city">{{ address.places[0]['place name'] }}</p>
      <p class="zip-code-finder__result-state">{{ address.places[0].state }}</p>
      <p class="zip-code-finder__result-other">long: {{ address.places[0].longitude }}</p>
      <p class="zip-code-finder__result-other">lat: {{ address.places[0].latitude }}</p>
      <button class="zip-code-finder__clear" @click="clearAddress">
        <svg stroke="currentColor" fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round" color="#FFF" height="25" width="25" xmlns="http://www.w3.org/2000/svg" style="color: rgb(255, 255, 255);">
          <circle cx="12" cy="12" r="10"></circle>
          <line x1="15" y1="9" x2="9" y2="15"></line>
          <line x1="15" y1="15" x2="9" y2="9"></line>
        </svg>
      </button>
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
    },
    clearAddress() {
      this.address = null;
      this.errorMessage = '';
    },
    async onSubmit(event) {
      event.preventDefault();
      await this.search();
    }
  }
};
</script>


<style>
.zip-code-finder {
  display: flex;
  flex-direction: column;

  height: 400px;
  margin-bottom: 20rem;
}

.zip-code-finder__form {
  display: flex;
  justify-content: center;
  align-items: center;

  background-color: hsla(0,0%,100%,.2);
  border-radius: 8px;
  box-shadow: 1px 3px 8px rgba(0,0,0,.5);

  margin: 34px 0;
  padding: 15px;

  transition: background .3s ease;
}

.zip-code-finder__form:hover {
  background-color: hsla(0,0%,65%,.2);
}

.zip-code-finder__input {
  margin-right: 10px;
  padding: 5px;
  border-radius: 5px;
  outline: none;
  background: transparent;
  color: white;
}



.zip-code-finder__button {
  color: white;
}

.zip-code-finder__result {
  margin-top: 10px;
  color: white;
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

.zip-code-finder__clear {
  margin-top: 15px;
}

.zip-code-finder__error {
  margin-top: 10px;
  color: red;
}
</style>

