<template>
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
</template>

<script>
export default {
  props: ['github_repos'],
};
</script>

<style lang="scss">
.content-repos-item {
  padding: 15px;
  background: #fff;
  transition: 250ms all;
  height: 110px;
  text-decoration: none;
  color: inherit;
  border-radius: 10px;
  box-shadow: 1px 3px 10px rgba(black, 0.2);

  h5 {
    color: #222;
    transition: 300ms color;
    margin-bottom: 6px;
  }
  span {
    display: block;
    font-size: 12px;
    line-height: 1.2;
    color: #333;
    transition: 300ms color;
  }

  &:hover {
    transform: scale(1.2);
    z-index: 4;

    h5 {
      color: purple;
    }
    span {
      color: teal;
    }
  }
}
</style>
