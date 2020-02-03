<template>
  <div id="app">
    <h1 class="title">Todo application</h1>
    <hr />

    <router-view />
  </div>
</template>



<style scoped>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  max-width: 1200px;
  margin: 0 auto;
}

.title {
  background-color: black;
  color: #fff;
}
</style>
