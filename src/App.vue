<template>
  <div id="app">
    <div class="background"></div>
    <div class="title-container">
      <h1 class="title">SENDI SATRIA PANGESTU</h1>
      <h2 class="subtitle">213510800 Find me on @thisis_shndy</h2>
    </div>
    <div class="content">
      <nav>
        <router-link to="/" class="nav-link">Cuaca</router-link> |
        <router-link to="/lokasi" class="nav-link">Lokasi</router-link> |
        <router-link to="/stopwatch" class="nav-link">StopWatch</router-link> |
        <router-link to="/foto" class="nav-link">Foto Random</router-link> |
        <router-link to="/TebakAngka" class="nav-link">Game Tebak Angka</router-link> |
        <router-link to="/PenjagaPintu" class="nav-link">Game Penjaga Pintu</router-link>
      </nav>
      <router-view/>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  min-height: 100vh;
}

.background {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: url('@/assets/background.GIF');
  background-size: cover;
  background-position: center;
  z-index: -1;
}

.title-container {
  text-align: center;
  margin-top: 80px;
  margin-bottom: 40px;
}

.title {
  font-size: 40px;
  color: #fff;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
  margin-bottom: 10px;
}

.subtitle {
  font-size: 18px;
  color: #eee;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
}

.content {
  max-width: 800px;
  margin: auto;
  padding: 20px;
  background-color: rgba(255, 255, 255, 0.9);
  border-radius: 8px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.3);
  text-align: center;
}

nav {
  padding: 20px 0;
  background-color: #3498db;
  display: flex;
  justify-content: center;
}

.nav-link {
  margin: 0 10px;
  font-weight: bold;
  color: #fff;
  text-decoration: none;
  transition: color 0.3s ease;
}

.nav-link:hover {
  color: #eee;
}

.nav-link.router-link-exact-active {
  color: #eee;
}
</style>
