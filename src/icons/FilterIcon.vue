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
    <path d="M14 6m-2 0a2 2 0 1 0 4 0a2 2 0 1 0 -4 0" />
    <path d="M4 6h8" />
    <path d="M16 6h4" />
    <path d="M8 12m-2 0a2 2 0 1 0 4 0a2 2 0 1 0 -4 0" />
    <path d="M4 12h2" />
    <path d="M10 12h10" />
    <path d="M17 18m-2 0a2 2 0 1 0 4 0a2 2 0 1 0 -4 0" />
    <path d="M4 18h11" />
    <path d="M19 18h1" />
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
