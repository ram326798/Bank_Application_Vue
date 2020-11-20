<template>
  <div id="app">
    <div id="nav">
      <h2>Bank Management</h2>
    </div>
    <router-view />
  </div>
</template>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #38b4f2;
  margin-left: auto;
  margin-right: auto;
}

#nav {
  padding: 15px;
}
</style>
