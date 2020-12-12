<template>
  <div class="profile-page" v-if="github_userdata && github_repos">
    <div class="sidebar">
      <!--SIDEBAR-->
      <div class="sidebar-profile">
        <div class="sidebar-profile-image">
          <img
            :src="github_userdata.avatar_url"
            :alt="github_userdata.username"
          />
        </div>
        <h2 class="sidebar-profile-username">
          {{ `${github_userdata.login}` }}
        </h2>

        <div class="sidebar-profile-stats">
          <div class="sidebar-profile-stats-follow">
            <span class="followers"
              >Followers
              <span class="count">{{ github_userdata.followers }}</span></span
            >
            <span class="following"
              >Following
              <span class="count">{{ github_userdata.following }}</span></span
            >
          </div>

          <div class="sidebar-profile-stats-repos">
            <span class="repos"
              >Public Repos<span class="count">{{
                github_userdata.public_repos
              }}</span></span
            >
            <span class="gists"
              >Public Gists
              <span class="count">{{
                github_userdata.public_gists
              }}</span></span
            >
          </div>
        </div>
        <div class="sidebar-profile-bio">
          <p class="text" v-if="github_userdata.bio">
            {{ github_userdata.bio }}
          </p>
          <p class="company" v-if="github_userdata.company">
            @{{ github_userdata.company }}
          </p>
        </div>
        <div class="sidebar-profile-date">
          <div class="created_at">
            updated at <i>{{ github_userdata.updated_at.substr(0, 10) }}</i>
          </div>
          <div class="created_at">
            created at <i>{{ github_userdata.created_at.substr(0, 10) }}</i>
          </div>
        </div>
      </div>
    </div>
    <!--CONTENT-->
    <div class="content">
      <div class="content-repos">
        <a
          v-for="repo in github_repos"
          :key="repo.id"
          class="content-repos-item"
          target="_blank"
          :href="repo.html_url"
        >
          <h5 class="content-repos-item-name">{{ repo.name }}</h5>

          <span v-if="repo.language" class="content-repos-item-lang"
            >language: {{ repo.language }}</span
          >
          <span class="content-repos-item-size">size: {{ repo.size }} KB</span>
          <span class="content-repos-item-watchers">
            watchers: {{ repo.watchers }}
          </span>
          <span v-if="repo.forks" class="content-repos-item-license"
            >forks: {{ repo.forks }}</span
          >
          <span v-if="repo.license" class="content-repos-item-license"
            >licence: {{ repo.license.key }}</span
          >
        </a>
      </div>
    </div>
  </div>
  <div class="loading-animation" v-else>
    <div class="loading-animation-container"><logo-daff /></div>
  </div>
</template>

<script>
import axios from 'axios';
import LogoDaff from '../components/LogoDaff.vue';
export default {
  components: { LogoDaff },
  data() {
    return {
      username: this.$route.params.username,
      github_userdata: {},
      github_repos: [],
    };
  },
  computed: {
    routeVal() {},
  },

  created() {
    if (this.username) {
      axios
        .get(`https://api.github.com/users/${this.username}`)
        .then((data) => {
          if (data.status === 200) this.github_userdata = data.data;
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
  // display: grid;
  // grid-template-columns: 1fr 4fr;
}

.sidebar {
  padding: 15px;
  position: fixed;
  background: #fff;
  height: 100vh;
  width: 250px;
  &-profile {
    &-image {
      width: 100%;
      height: 100%;
      overflow: hidden;
      img {
        width: 100%;
        height: auto;
      }
    }
    &-bio {
      margin-top: 15px;
      font-size: 14px;
      .company {
        font-weight: bold;
        margin-top: 15px;
      }
    }
    &-username {
      color: #222;
      margin-top: 15px;
      margin-bottom: 15px;
    }
    &-stats {
      &-follow {
        display: flex;
        .followers,
        .following {
          width: 100%;
          display: flex;
          flex-direction: column;
          font-size: 10px;
          background: #222;
          color: #fff;
          padding: 3px 6px;
          margin: 2px;
          .count {
            font-size: 16px;
          }
        }
      }

      &-repos {
        display: flex;

        .repos,
        .gists {
          width: 100%;
          display: flex;
          flex-direction: column;
          font-size: 10px;
          background: #222;
          color: #fff;
          padding: 3px 6px;
          margin: 2px;
          .count {
            font-size: 16px;
          }
        }
      }
    }
    &-date {
      margin-top: 30px;
      font-size: 12px;
      color: #444;
    }
  }
}
.content {
  padding: 15px;
  margin-left: 250px;
  &-repos {
    grid-gap: 15px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    flex-wrap: wrap;
    &-item {
      border: 1px solid black;
      padding: 15px;
      background: #fff;
      transition: 250ms;
      height: 110px;
      text-decoration: none;
      color: inherit;
      &:hover {
        transform: scale(1.2);
        z-index: 4;
        h5 {
          color: black;
        }
        span {
          color: #222;
        }
      }
      h5 {
        color: #222;
        transition: 250ms;
        margin-bottom: 6px;
      }
      span {
        display: block;
        font-size: 12px;
        line-height: 1.2;
        color: #333;
        transition: 250ms;
      }
    }
  }
}
</style>
