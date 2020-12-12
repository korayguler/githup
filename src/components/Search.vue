<template>
  <div class="ui big search">
    <div class="ui icon input">
      <input
        class="prompt"
        type="text"
        v-model="usernameInput"
        placeholder="@username"
        @keydown.enter="
          $router.push(
            `/${usernameInput
              .toString()
              .toLowerCase()
              .replace(' ', '')}`,
          )
        "
      />
      <span class="search-icon"> <i class="fas fa-search"></i></span>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      usernameInput: '',
    };
  },
};
</script>

<style>
.search-icon {
  position: absolute;
  right: 20px;
  top: 50%;
  transform: translateY(-50%);
  color: #c7c7c7;
}
</style>
