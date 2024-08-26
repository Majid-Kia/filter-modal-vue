<template>
  <svg
    xmlns="http://www.w3.org/2000/svg"
    :width="width"
    :height="height"
    viewBox="0 0 24 24"
    fill="none"
    stroke="currentColor"
    :stroke-width="strokeWidth"
    stroke-linecap="round"
    stroke-linejoin="round"
    :class="className"
  >
    <path stroke="none" d="M0 0h24v24H0z" fill="none" />
    <path d="M12 5l0 14" />
    <path d="M5 12l14 0" />
  </svg>
</template>

<script>
export default {
  props: {
    width: {
      type: [String, Number],
      default: 20,
    },
    height: {
      type: [String, Number],
      default: 20,
    },
    strokeWidth: {
      type: [String, Number],
      default: 2,
    },
    className: {
      type: String,
      default: "",
    },
  },
};
</script>

<style scoped></style>
