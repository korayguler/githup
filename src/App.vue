<template>
  <div class="main">
    <router-link to="/" class="go-back-button">
      <a>go back</a>
    </router-link>
    <div class="layout">
      <router-view />
    </div>
  </div>
</template>

<style lang="scss">
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

  .main {
    .go-back-button {
      position: fixed;
      bottom: 20px;
      right: 20px;
      background: #222222;
      padding: 10px 20px;
      border-radius: 4px;
      text-decoration: none;
      color: #fff;
    }
  }
}
</style>
