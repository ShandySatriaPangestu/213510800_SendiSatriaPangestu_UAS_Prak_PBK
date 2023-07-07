<template>
  <div class="photo-widget">
    <h2>{{ title }}</h2>
    <div class="photo-container">
      <img :src="photoUrl" :alt="title" />
    </div>
    <button @click="getRandomPhoto" class="load-button">Load Foto Foto Random Disini</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: '',
      photoUrl: '',
    };
  },
  mounted() {
    this.getRandomPhoto();
  },
  methods: {
    async getRandomPhoto() {
      try {
        const apiKey = 'KF6xmlsA8ansrm3sK6qQeGep8IFbrRVf5kb3tX37Yx0';
        const apiUrl = `https://api.unsplash.com/photos/random?client_id=${apiKey}&query=nature`;

        const response = await fetch(apiUrl);
        const data = await response.json();

        this.title = data.description || 'Untitled';
        this.photoUrl = data.urls.regular;
      } catch (error) {
        console.error('Error fetching random photo:', error);
      }
    },
  },
};
</script>

<style scoped>
.photo-widget {
  border: 2px solid black;
  padding: 20px;
  margin-bottom: 20px;
  background-color: lightgray;
  border-radius: 8px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.photo-widget h2 {
  color: #333;
  font-size: 24px;
  margin-bottom: 10px;
}

.photo-container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  max-width: 500px;
  margin-top: 10px;
}

.photo-container img {
  max-width: 100%;
  max-height: 100%;
}

.load-button {
  padding: 10px 20px;
  background-color: #2980b9;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  margin-top: 10px;
}

.load-button:hover {
  background-color: #5da4d3;
}
</style>
