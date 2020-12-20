<template>
  <router-link to="/homepage">link</router-link>
  <router-link to="/projects">link</router-link>
  <router-view />
</template>
<style>
*,
*:before,
*:after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  @import url('https://fonts.googleapis.com/css2?family=Fira+Code:wght@300;400;500;600&display=swap');
  font-family: 'Fira Code', monospace;
}
#app {
  height: 100vh;
}
</style>
