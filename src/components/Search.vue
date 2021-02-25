<template>
  <span class="logo">
    <img src="images/Fintechtocat.png" alt="" />
  </span>
  <div class="search">
    <input
      class="prompt search-input"
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

<style lang="scss">
.logo {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  height: 100vh;
  transform-origin: center;
  img {
    height: 100%;
    width: auto;

    animation: rotate 12s infinite alternate-reverse;
  }
}

@keyframes rotate {
  from {
    transform: rotate(-90deg);
  }

  to {
    transform: rotate(90deg);
  }
}

.search {
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 250px;

  &-logo {
    width: 50%;
  }
  &-input {
    width: 100%;
    height: 50px;
    font-size: 20px;
    padding-left: 20px;
    font-weight: 100;
    color: #222;
    outline: none;
    border: none;
    border-radius: 50px;
    box-shadow: 2px 6px 10px rgba(0, 0, 0, 0.2);
    background: rgba(255, 255, 255, 0.5);

    &::placeholder {
      color: #222;
    }
  }
}
</style>
