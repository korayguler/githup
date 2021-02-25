<template>
  <div>
    <div class="layout">
      <router-view />
    </div>
  </div>
</template>

<style>
*,
*:before,
*:after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.layout {
  z-index: 6;
}

@keyframes hue {
  from {
    filter: hue-rotate(0);
  }
  to {
    filter: hue-rotate(360deg);
  }
}

body {
  @import url('https://fonts.googleapis.com/css2?family=Fira+Code:wght@300;400;500;600&display=swap');
  font-family: 'Fira Code', monospace;
}
#app {
  height: 100vh;
}
</style>
