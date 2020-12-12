<template>
  <div class="home">
    <LogoDaff />
    <Search />
  </div>
</template>

<script>
// @ is an alias to /src
import Search from '@/components/Search.vue';
import LogoDaff from '@/components/LogoDaff.vue';

export default {
  name: 'Home',
  components: {
    Search,
    LogoDaff,
  },
};
</script>

<style>
.home {
  width: 100vw;
  height: 100vh;
  grid-template-columns: 1fr 1fr;
  display: grid;
  align-items: center;
}
</style>
