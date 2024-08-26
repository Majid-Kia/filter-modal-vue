<template>
  <div>
    <button @click="openModal" class="modal-btn">
      <span> فیلتر‌ها</span>
      <FilterIcon class="blue" />
    </button>
    <FilterModal
      v-if="showModal"
      :filters="filterData.filters"
      :selectedFilters="selectedFilters"
      @setFilters="setSelectedFilters"
      @close="closeModal"
      @clearAllFilters="clearAllFilters"
    />
    <SelectedFilterTags
      v-if="Object.keys(selectedFilters).length > 0"
      :filters="filterData.filters"
      :selectedFilters="selectedFilters"
      @removeFilter="removeSelectedFilter"
      @clearAllFilters="clearAllFilters"
    />
  </div>
</template>

<script>
import FilterIcon from "@/icons/FilterIcon.vue";
import FilterModal from "./FilterModal.vue";
import SelectedFilterTags from "./SelectedFilterTags.vue";

export default {
  props: {
    filterData: Object,
  },
  components: {
    FilterIcon,
    FilterModal,
    SelectedFilterTags,
  },
  data() {
    return {
      showModal: false,
      selectedFilters: {},
    };
  },
  methods: {
    openModal() {
      this.showModal = true;
    },
    closeModal() {
      this.showModal = false;
    },
    setSelectedFilters(filters) {
      this.selectedFilters = filters;
    },
    removeSelectedFilter(filterKey, id) {
      // Remove a specific filter by key and id
      const updatedSelections = this.selectedFilters[filterKey].filter(
        (item) => item.id !== id
      );

      if (updatedSelections.length === 0) {
        // Delete filter group if empty
        this.$delete(this.selectedFilters, filterKey);
      } else {
        // Update filter group with remaining selections
        this.$set(this.selectedFilters, filterKey, updatedSelections);
      }

      // Check if any filters are still selected; if none, clear all filters
      if (Object.keys(this.selectedFilters).length === 0) {
        this.clearAllFilters();
      }
    },
    clearAllFilters() {
      this.selectedFilters = {};
    },
  },
};
</script>

<style lang="scss" scoped>
.modal-btn {
  border: 1px solid $gray;
  color: $navy;
  height: 3rem;
  border-radius: 0.375rem;
  padding-left: 1rem;
  padding-right: 1rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  cursor: pointer;
  span {
    margin-left: 0.5rem;
  }
}
</style>
