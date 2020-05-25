<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <main>
      <router-view/>
    </main>
  </div>
</template>

<script>

export default {
  name: 'App'
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;

  background-image: url('./assets/gumbole.jpeg');
  background-size: cover;
  background-position: top;
  transition: 0.4s;
}

main {
  min-height: 100vh;
  padding: 3rem;

  background-image: linear-gradient(to bottom, rgba(0, 0,0 , 0.25), rgba(0, 0, 0, 0.75));
}

main > div {
  min-height: 80vh;
}
</style>
