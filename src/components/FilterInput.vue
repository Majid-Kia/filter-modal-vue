<template>
  <input
    v-if="filter.hasSearch"
    type="text"
    placeholder="جستجو..."
    class="input"
    @input="search"
  />
</template>

<script>
export default {
  props: {
    filter: Object,
  },
  methods: {
    search(event) {
      this.$emit("search", this.filter.filterKey, event.target.value);
    },
  },
};
</script>

<style scoped lang="scss">
.input {
  width: 100%;
  padding: 0.5rem;
  border: 1px solid $gray;
  border-radius: 4px;
  font-size: 1rem;
  font-family: inherit;
}
</style>
