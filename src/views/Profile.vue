<template>
  <div
    class="profile-page"
    v-if="github_userdata && github_repos && !isLoading"
  >
    <Sidebar :github_userdata="github_userdata" />
    <Repos :github_repos="github_repos" />
  </div>

  <div class="loading-animation" v-if="isLoading">
    <div class="loading-animation-container"><h1>Loading...</h1></div>
  </div>
  <page-title :title="`${this.$route.params.username} | githup`" />
</template>

<script>
import axios from 'axios';
import PageTitle from '@/components/PageTitle';
import Repos from '@/components/Repos.vue';
import Sidebar from '@/components/Sidebar.vue';
export default {
  components: { Repos, Sidebar, PageTitle },

  data() {
    return {
      username: this.$route.params.username,
      github_userdata: {},
      github_repos: [],
      isLoading: true,
    };
  },
  methods: {},
  mounted() {
    if (!this.username) {
      router.push('/');
    } else {
      axios
        .get(`https://api.github.com/users/${this.username}`)
        .then((data) => {
          if (data.status === 200) this.github_userdata = data.data;
          this.isLoading = false;
        })
        .catch((err) => {
          this.$router.push('/');
          console.log(err);
        });
      axios
        .get(`https://api.github.com/users/${this.username}/repos`)
        .then((data) => {
          if (data.status === 200) {
            this.github_repos = data.data;
            console.log(data.data);
          }
        })
        .catch((err) => {
          console.log(err);
        });
    }
  },
};
</script>

<style lang="scss">
.loading-animation {
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100vw;
  height: 100vh;
  background: #fff;
  &-container {
    width: 200px;
    height: auto;
  }
}
.profile-page {
  height: 100vh;
  max-width: 1366px;
  margin-right: auto;
  margin-left: auto;
}
</style>
