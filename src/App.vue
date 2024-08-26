<template>
  <div id="app">
    <div class="container">
      <BaseFilter :filterData="filterData" />
    </div>
  </div>
</template>

<script>
import BaseFilter from "@/components/BaseFilter.vue";
import filterData from "@/constants/filters.json";

export default {
  components: {
    BaseFilter,
  },
  data() {
    return {
      filterData,
    };
  },
};
</script>

<style lang="scss" scoped>
.container {
  max-width: 900px;
  padding: 16px;
  margin: auto;
}
.filte-btn {
  border: 1px solid #d1d5db;
  color: #1f2937;
  height: 3rem;
  border-radius: 0.375rem;
  padding-left: 1rem;
  padding-right: 1rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  cursor: pointer;
}
</style>
