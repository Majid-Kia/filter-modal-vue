<template>
  <div class="accordion">
    <button @click="onToggle">
      {{ title }}
      <PlusIcon v-if="isOpen" />
      <MinusIcon v-else />
    </button>
    <div v-if="isOpen" class="accordion-content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import PlusIcon from "@/icons/MinusIcon.vue";
import MinusIcon from "@/icons/PlusIcon.vue";
export default {
  props: {
    title: String,
    isOpen: Boolean,
  },
  components: {
    PlusIcon,
    MinusIcon,
  },

  methods: {
    onToggle() {
      this.$emit("toggle");
    },
  },
};
</script>

<style scoped lang="scss">
.accordion-content {
  padding: 1rem;
}
.accordion {
  button {
    width: 100%;
    display: flex;
    justify-content: space-between;
    font-size: 1rem;
    padding: 1rem;
    transition: 300ms;
    cursor: pointer;
    border-radius: 8px;
    color: $navy;
    &:hover {
      background-color: $grayLight;
    }
  }
}
</style>
