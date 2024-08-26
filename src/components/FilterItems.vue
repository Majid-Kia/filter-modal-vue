<template>
  <div class="filter-items">
    <div
      v-for="item in filteredItems"
      :key="item.id"
      class="filter-items__item"
    >
      <!-- If the item has child items, display them -->
      <div v-if="item.childs && item.childs.length">
        <span class="filter-items__item_name">{{ item.name }}</span>
        <div
          v-for="child in item.childs"
          :key="child.id"
          class="filter-item__list"
        >
          <label class="flex items-center">
            <input
              :type="filter.mode === 'single' ? 'radio' : 'checkbox'"
              :name="filter.filterKey"
              :checked="isSelected(child.id)"
              @change="toggleItemSelection(child)"
            />
            <span>{{ child.name }}</span>
          </label>
        </div>
      </div>

      <!-- If no child items, render the item directly -->
      <label v-else class="flex items-center">
        <input
          :type="filter.mode === 'single' ? 'radio' : 'checkbox'"
          :name="filter.filterKey"
          :checked="isSelected(item.id)"
          @change="toggleItemSelection(item)"
        />
        <span>{{ item.name }}</span>
      </label>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    filter: Object,
    selectedFilters: Object,
    searchQueries: Object,
  },
  computed: {
    filteredItems() {
      // Filters items based on the current search query
      const query =
        this.searchQueries[this.filter.filterKey]?.toLowerCase() || "";

      // Return only the items that match the search query
      return this.filter.items.filter((item) => {
        return item.name.toLowerCase().includes(query);
      });
    },
  },
  methods: {
    isSelected(id) {
      return this.selectedFilters[this.filter.filterKey]?.some(
        (item) => item.id === id
      );
    },
    toggleItemSelection(item) {
      this.$emit(
        "toggleSelection",
        this.filter.filterKey,
        item,
        this.filter.mode
      );
    },
  },
};
</script>

<style scoped lang="scss">
.filter-items__item {
  margin-top: 0.5rem;
  display: flex;
}
.filter-item__list {
  margin-right: 1rem;
}
label {
  font-size: 14px;
  margin-top: 0.25rem;
  color: $navy;
  cursor: pointer;
}
.filter-items__item_name {
  margin-top: 1rem;
  display: flex;
}
</style>
