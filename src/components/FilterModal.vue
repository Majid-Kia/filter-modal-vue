<template>
  <div class="modal-wrapper">
    <div class="modal-content">
      <h2 class="">فیلتر‌ها</h2>
      <SelectedFilterTags
        :filters="filters"
        :selectedFilters="selectedFilters"
        @removeFilter="removeSelectedFilter"
        @clearAllFilters="clearAllFilters"
      />
      <BaseAccordion
        v-for="filter in filters"
        :key="filter.filterKey"
        :title="filter.title"
        :isOpen="activeAccordion === filter.filterKey"
        @toggle="toggleAccordion(filter.filterKey)"
      >
        <FilterInput :filter="filter" @search="handleSearch" />
        <FilterItems
          :filter="filter"
          :selectedFilters="selectedFilters"
          @toggleSelection="toggleSelection"
          :searchQueries="searchQueries"
        />
      </BaseAccordion>

      <div class="add-filter">
        <button
          class="bg-blue-400 text-white rounded h-12 px-4"
          @click="applyFilters"
        >
          اعمال فیلتر‌ها
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import SelectedFilterTags from "./SelectedFilterTags.vue";
import BaseAccordion from "./BaseAccordion.vue";
import FilterItems from "./FilterItems.vue";
import FilterInput from "./FilterInput.vue";
export default {
  props: {
    filters: Array,
    selectedFilters: Object,
  },
  components: {
    SelectedFilterTags,
    BaseAccordion,
    FilterItems,
    FilterInput,
  },
  data() {
    return {
      activeAccordion: null,
      searchQueries: {},
    };
  },
  methods: {
    toggleSelection(filterKey, item, mode) {
      // Handle selecting or deselecting items, updating selectedFilters
      const selected = this.selectedFilters[filterKey] || [];

      let newSelections;

      if (mode === "single") {
        // In single-select mode, replace the entire selection with the new item
        newSelections = [item];
      } else {
        // In multi-select mode, toggle the selection of the item
        const exists = selected.some((selection) => selection.id === item.id);
        newSelections = exists
          ? selected.filter((selection) => selection.id !== item.id)
          : [...selected, item];
      }

      this.$set(this.selectedFilters, filterKey, newSelections);
    },
    handleSearch(filterKey, query) {
      this.$set(this.searchQueries, filterKey, query);
    },
    removeSelectedFilter(filterKey, id) {
      const updatedSelections = this.selectedFilters[filterKey].filter(
        (item) => item.id !== id
      );

      if (updatedSelections.length === 0) {
        // If no more selections in the filter group, remove the entire key
        this.$delete(this.selectedFilters, filterKey);
      } else {
        // Otherwise, update the filter group with the new selections
        this.$set(this.selectedFilters, filterKey, updatedSelections);
      }

      // Check if any filters are still selected; if none, clear all filters
      if (Object.keys(this.selectedFilters).length === 0) {
        this.clearAllFilters();
      }
    },
    applyFilters() {
      this.$emit("close");
    },
    toggleAccordion(filterKey) {
      this.activeAccordion =
        this.activeAccordion === filterKey ? null : filterKey;
    },
    clearAllFilters() {
      this.$emit("clearAllFilters");
    },
  },
};
</script>

<style lang="scss" scoped>
.add-filter {
  display: flex;
  justify-content: center;
  margin-top: 2rem;
  button {
    background-color: $blue;
    color: $white;
    border-radius: 0.25rem;
    height: 3rem;
    padding: 0 1rem;
  }
}
.modal-wrapper {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background-color: rgba($black, 0.65);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 50;
}
.modal-content {
  background-color: white;
  width: 100%;
  max-width: 64rem;
  height: 100%;
  padding: 1rem 3rem;
  border-radius: 0.5rem;
  overflow-y: auto;
  h2 {
    font-weight: 400;
    font-size: 1.5rem;
    color: $navy;
  }
}
</style>
