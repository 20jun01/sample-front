import HeaderMap from '@/components/HeaderMap.vue';
<template>
  <v-app>
    <div id="app">
      <v-system-bar fixed height="40" color="green lighten-1" lights-out dark>
        random飲食店
        <v-spacer></v-spacer>
        <v-btn plain to="/"><v-icon>mdi-home</v-icon></v-btn>
        <v-btn plain to="/about"><v-icon>mdi-heart</v-icon></v-btn>
        <v-btn plain to="/result"><v-icon>mdi-map-marker</v-icon></v-btn>
      </v-system-bar>
      <div class="router">
        <router-view />
      </div>
    </div>
  </v-app>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}

div {
  &.router {
    margin-top: 40px;
  }
}

@media (min-height: 700px) {
  #unscrollable {
    position: fixed;
    width: 100%;
  }
}
</style>