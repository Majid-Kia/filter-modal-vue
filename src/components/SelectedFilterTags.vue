<template>
  <div class="selected-filters">
    <span
      v-for="(values, filterKey) in selectedFilters"
      :key="filterKey"
      class="filter-chips"
    >
      <span v-for="value in values" :key="value.id" class="filter-chip__name">
        {{ value.name }}
        <span
          class="filter-chip__icon"
          @click="removeFilter(filterKey, value.id)"
        >
          <CloseIcon />
        </span>
      </span>
    </span>
    <button
      v-if="Object.keys(selectedFilters).length > 0"
      @click="clearAllFilters"
      class="remove-all-filters"
    >
      پاک کردن همه فیلترها
    </button>
  </div>
</template>

<script>
import CloseIcon from "@/icons/CloseIcon.vue";
export default {
  props: {
    filters: Array,
    selectedFilters: Object,
  },
  components: {
    CloseIcon,
  },
  methods: {
    removeFilter(filterKey, valueId) {
      this.$emit("removeFilter", filterKey, valueId);
    },
    clearAllFilters() {
      this.$emit("clearAllFilters");
    },
  },
};
</script>

<style scoped lang="scss">
.selected-filters {
  margin-bottom: 2rem;
  display: flex;
  flex-wrap: wrap;
  position: relative;
}

.filter-chips {
  display: flex;
  margin: 0.25rem;
  flex-wrap: wrap;
}
.filter-chip__name {
  @media (min-width: 640px) {
    padding: 0.5rem 0.75rem;
  }
  align-items: center;
  padding: 0.25rem 0.5rem;
  border-radius: 9999px;
  display: flex;
  margin-left: 0.5rem;
  margin-bottom: 0.5rem;
  align-items: center;
  background-color: $grayLight;
  &:hover {
  }
  border-radius: 40px;
  font-size: 14px;
}
.filter-chip__icon {
  display: flex;
  align-items: center;
  margin-right: 0.5rem;
  cursor: pointer;
  transition: 300ms;
  &:hover {
    background-color: $gray;
    border-radius: 100%;
  }
}
.remove-all-filters {
  padding: 0.5rem;
  border-radius: 4px;
  cursor: pointer;
  transition: 300ms;
  position: absolute;
  border: 1px solid $gray;
  left: 0;
  top: -40px;
  &:hover {
    background-color: $grayLight;
  }
}
</style>
