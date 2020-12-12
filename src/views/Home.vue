<template>
  <div class="home">
    <Search />
  </div>
</template>

<script>
// @ is an alias to /src
import Search from '@/components/Search.vue';

export default {
  name: 'Home',
  components: {
    Search,
  },
};
</script>

<style>
.home {
  width: 100vw;
  height: 100vh;
  position: relative;
}
</style>
