<template>
  <div class="sidebar">
    <!--SIDEBAR-->
    <div class="sidebar-profile">
      <div class="sidebar-profile-image">
        <img :src="githubUserData.avatar_url" :alt="githubUserData.username" />
      </div>
      <h2 class="sidebar-profile-username">
        {{ `${githubUserData.login}` }}
      </h2>

      <div class="sidebar-profile-stats">
        <div class="sidebar-profile-stats-follow">
          <span class="followers"
            >Followers
            <span class="count">{{ githubUserData.followers }}</span></span
          >
          <span class="following"
            >Following
            <span class="count">{{ githubUserData.following }}</span></span
          >
        </div>

        <div class="sidebar-profile-stats-repos">
          <span class="repos"
            >Public Repos<span class="count">{{
              githubUserData.public_repos
            }}</span></span
          >
          <span class="gists"
            >Public Gists
            <span class="count">{{ githubUserData.public_gists }}</span></span
          >
        </div>
      </div>
      <div class="sidebar-profile-bio">
        <p class="text" v-if="githubUserData.bio">
          {{ githubUserData.bio }}
        </p>
        <p class="company" v-if="githubUserData.company">{{ company }}</p>
      </div>
      <div class="sidebar-profile-date">
        <div class="created_at">
          updated at <i>{{ githubUserData.updated_at?.substr(0, 10) }}</i>
        </div>
        <div class="created_at">
          created at <i>{{ githubUserData.created_at?.substr(0, 10) }}</i>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['githubUserData'],
  computed: {
    company() {
      if (this.githubUserData.company?.toString().includes('@', 0)) {
        return this.githubUserData.company?.toString();
      } else {
        return `@${this.githubUserData.company?.toString()}`;
      }
    },
  },
};
</script>

<style lang="scss">
.sidebar {
  padding: 15px;
  position: fixed;
  background: #fff;
  height: 100vh;
  width: 250px;
  box-shadow: 1px 0 10px rgba(black, 0.2);
  overflow-y: scroll;

  @media only screen and (max-width: 800px) {
    position: static;
    width: 100%;
    overflow: hidden;
    padding: 30px;
    margin-bottom: 30px;
    height: auto;
  }

  &-profile {
    &-image {
      width: 100%;
      height: 100%;
      overflow: hidden;
      transition: 300ms all;
      &:hover {
        transform: scale(1.03);
      }
      img {
        width: 100%;
        height: auto;
        border-radius: 13px;
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
      .followers,
      .following,
      .repos,
      .gists {
        transition: 300ms all;

        &:hover {
          transform: scale(1.03);
        }
      }
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
          border-radius: 5px;
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
          border-radius: 5px;

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
</style>
