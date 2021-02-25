<script>
export default {
  name: 'vue-title',
  props: ['title'],
  watch: {
    title: {
      immediate: true,
      handler() {
        document.title = this.title;
      },
    },
  },
  render() {},
};
</script>
