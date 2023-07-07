<template>
  <div class="location-widget">
    <h2 class="widget-title">Your Location</h2>
    <div class="widget-content">
      <div class="location-coordinates">
        <div v-if="latitude && longitude" class="coordinates-info">
          <p>Garis Lintang : {{ latitude }}</p>
          <p>Garis Bujur   : {{ longitude }}</p>
        </div>
        <div v-else>
          <p>Finding your location...</p>
        </div>
      </div>
      <div class="location-inputs">
        <div class="location-input">
          <label for="latitude">Garis Lintang:</label>
          <input type="text" id="latitude" v-model="inputLatitude" />
        </div>
        <div class="location-input">
          <label for="longitude">Garis Bujur:</label>
          <input type="text" id="longitude" v-model="inputLongitude" />
        </div>
      </div>
    </div>
    <button @click="fetchLocationDetails" class="find-button">Find Location Details</button>
    <div v-if="foundLocation" class="location-details">
      <h3>Location Details</h3>
      <p>{{ foundLocation.components.country }}</p>
      <p>{{ foundLocation.components.city }}</p>
      <p>{{ foundLocation.components.street }}</p>
      <p>Postal Code: {{ foundLocation.components.postcode }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      latitude: null,
      longitude: null,
      inputLatitude: '',
      inputLongitude: '',
      foundLocation: null,
    };
  },
  mounted() {
    if (navigator.geolocation) {
      navigator.geolocation.getCurrentPosition(this.getPosition);
    }
  },
  methods: {
    getPosition(position) {
      this.latitude = position.coords.latitude;
      this.longitude = position.coords.longitude;
    },
    async fetchLocationDetails() {
      try {
        const apiKey = '92591005a7b94008909d59a64b6d2a49';
        const latitude = this.inputLatitude || this.latitude;
        const longitude = this.inputLongitude || this.longitude;
        const apiUrl = `https://api.opencagedata.com/geocode/v1/json?q=${encodeURIComponent(
          latitude + ',' + longitude
        )}&key=${apiKey}`;

        const response = await fetch(apiUrl);
        const data = await response.json();

        if (data.results && data.results.length > 0) {
          const location = data.results[0];
          this.foundLocation = location;
          console.log('Location:', location);
          // Lakukan sesuatu dengan data lokasi yang ditemukan
        }
      } catch (error) {
        console.error('Error fetching location data:', error);
      }
    },
  },
};
</script>

<style scoped>
.location-widget {
  border: 2px solid #3498db;
  padding: 20px;
  margin-bottom: 20px;
  text-align: center;
  background-color: #f0f6fc;
  border-radius: 8px;
}

.widget-title {
  margin-top: 0;
  color: #3498db;
  font-size: 24px;
  font-weight: bold;
  text-transform: uppercase;
}

.widget-content {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  margin-bottom: 20px;
}

.location-coordinates {
  flex: 1;
  margin-right: 20px;
}

.coordinates-info p {
  color: #666;
  margin: 0;
}

.location-inputs {
  flex: 1;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.location-input {
  margin: 10px;
}

.location-input label {
  display: block;
  margin-bottom: 5px;
  color: #333;
  font-size: 16px;
}

.location-input input {
  padding: 8px 12px;
  font-size: 16px;
  width: 100px;
  text-align: center;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.find-button {
  padding: 10px 20px;
  background-color: #3498db;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.find-button:hover {
  background-color: #2980b9;
}

.location-details {
  margin-top: 20px;
  text-align: left;
}

.location-details h3 {
  margin-bottom: 10px;
  color: #333;
  font-size: 18px;
}

.location-details p {
  margin: 5px 0;
  color: #666;
}
</style>
