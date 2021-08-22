<template>
  <div class="content">
    <div class="content-repos">
      <Repo :githubRepos="githubRepos" />
    </div>
  </div>
</template>

<script>
import Repo from '@/components/Repo';
export default {
  components: { Repo },
  props: ['githubRepos'],
};
</script>

<style lang="scss">
.content {
  padding: 15px;
  margin-left: 250px;

  &-repos {
    grid-gap: 15px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);

    @media only screen and (max-width: 1200px) {
      grid-template-columns: repeat(3, 1fr);
    }

    @media only screen and (max-width: 1000px) {
      grid-template-columns: repeat(2, 1fr);
    }

    @media only screen and (max-width: 800px) {
      grid-template-columns: repeat(2, 1fr);
    }

    @media only screen and (max-width: 600px) {
      grid-template-columns: repeat(1, 1fr);
    }
  }

  @media only screen and (max-width: 800px) {
    margin-left: auto;
  }
}
</style>
