<script setup lang="ts">
import TransactionItem from "./transaction-item.vue";

import type { Transaction } from "@/types/types";

// Props
defineProps<{
  transactions: Transaction[];
  handleDelete: (id: string) => void;
}>();
</script>

<template>
  <div>
    <h3>History</h3>
    <ul class="list">
      <TransactionItem
        v-for="transaction in transactions"
        :key="transaction.id"
        :transaction="transaction"
        :handle-delete="handleDelete"
      />
    </ul>
  </div>
</template>

<style scoped>
.list {
  list-style-type: none;
  padding: 0;
  margin-bottom: 40px;
}
</style>
