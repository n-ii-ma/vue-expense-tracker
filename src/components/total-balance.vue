<script setup lang="ts">
import { computed } from "vue";

// Props
const props = defineProps({
  total: {
    type: Number,
    default: 0,
  },
});

// Specify the sign of the total
const sign = computed(() => (props.total < 0 ? "-" : ""));
</script>

<template>
  <h4>Your Balance</h4>
  <h1>{{ sign }}${{ Math.abs(total).toFixed(2) }}</h1>
</template>
