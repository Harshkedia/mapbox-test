<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Record</router-link> |
      <router-link to="/play">Play</router-link>
    </div>
    <transition name="fade">
      <router-view />
    </transition>
  </div>
</template>

<style>
@import "https://api.mapbox.com/mapbox-gl-js/v1.11.0/mapbox-gl.css";

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0 auto;
  padding: 20px;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

.fade-enter-active,
.fade-leave-active {
  transition-property: opacity;
  transition-duration: 0.25s;
}
.fade-enter-active {
  transition-delay: 0.25s;
}
.fade-enter,
.fade-leave-active {
  opacity: 0;
}
</style>
