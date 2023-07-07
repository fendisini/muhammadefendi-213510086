<template>
    <div class="location-widget">
      <h2>Your Location</h2>
      <div v-if="latitude && longitude">
        <p>Latitude: {{ latitude }}</p>
        <p>Longitude: {{ longitude }}</p>
      </div>
      <div v-else>
        <p>Finding your location...</p>
      </div>
  
      <button @click="fetchLocationDetails">Open Maps</button>
  
      <div v-if="foundLocation">
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
      fetchLocationDetails() {
        const googleMapsUrl = `https://www.google.com/maps/search/?api=1&query=${this.latitude},${this.longitude}`;
        window.open(googleMapsUrl, '_blank');
      },
    },
  };
  </script>
  
  <style scoped>
  .location-widget {
    border: 1px solid #ccc;
    padding: 20px;
    margin-bottom: 20px;
    text-align: center;
    background-color: #f5f5f5;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }

  .location-widget h2 {
    color: #333;
    font-size: 24px;
    margin-bottom: 20px;
  }
  
  .location-widget p {
    color: #666;
  }

  </style>
  