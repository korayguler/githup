<template>
  <div class="home">
    <Search />
  </div>
  <page-title :title="`Githup · type @username`" />
  <div class="animating-bg"></div>
</template>

<script>
import Search from '@/components/Search.vue';
import PageTitle from '@/components/PageTitle.vue';

export default {
  name: 'Home',
  components: {
    Search,
    PageTitle,
  },
};
</script>

<style>
.home {
  width: 100vw;
  height: 100vh;
  position: relative;
  z-index: 5;
  overflow: hidden;
}

.animating-bg {
  width: 100vw;
  height: 100vh;
  background-image: url(/images/bg.png);
  background-size: cover;
  overflow: hidden;
  position: absolute;
  z-index: 1;
  top: 0;
  left: 0;

  animation: 10s hue infinite alternate;
}

.animating-bg:after {
  content: '';
  width: 100%;
  height: 100%;
  position: absolute;
  background: inherit;
  z-index: -1;
  top: 0;
  left: 0;
  filter: blur(3px);
  transform: scale(1.3);
}
</style>
