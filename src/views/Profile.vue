<template>
  <div class="profile-page" v-if="!isLoading">
    <Sidebar :githubUserData="githubUserData" />
    <Repos :githubRepos="githubRepos" />
  </div>

  <div class="loading-animation" v-if="isLoading">
    <div class="loading-animation-container"><h1>Loading...</h1></div>
  </div>
  <page-title :title="`<${this.$route.params.username}/>`" />
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
      githubUserData: {},
      githubRepos: [],
      userIsLoading: true,
      reposIsLoading: true,
    };
  },
  computed: {
    isLoading() {
      if (!this.userIsLoading && !this.reposIsLoading) return false;
      else return true;
    },
  },
  mounted() {
    if (!this.username) {
      router.push('/');
      return;
    }
    axios
      .get(`https://api.github.com/users/${this.username}`)
      .then((data) => {
        if (data.status === 200) {
          this.githubUserData = data.data;
          this.userIsLoading = false;
        }
      })
      .catch(() => this.$router.push('/'));

    axios
      .get(
        `https://api.github.com/users/${this.username}/repos?page=1&per_page=100`,
      )
      .then((data) => {
        if (data.status === 200) {
          this.githubRepos = data.data;
          this.reposIsLoading = false;
        }
      });
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
