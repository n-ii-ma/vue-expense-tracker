<script setup lang="ts">
import type { Transaction } from "@/types/types";

// Props
defineProps<{
  transaction: Transaction;
  handleDelete: (id: string) => void;
}>();
</script>

<template>
  <li :class="transaction.amount < 0 ? 'minus' : 'plus'">
    {{ transaction.title }}
    <div>
      <span v-if="transaction.amount < 0">-</span>
      <span v-else>+</span>
      <span>${{ Math.abs(transaction.amount).toFixed(2) }}</span>
    </div>
    <button class="delete-btn" @click="handleDelete(transaction.id)">x</button>
  </li>
</template>

<style scoped>
li {
  background-color: #fff;
  box-shadow: var(--box-shadow);
  color: #333;
  display: flex;
  justify-content: space-between;
  position: relative;
  padding: 10px;
  margin: 10px 0;
}

li.plus {
  border-right: 5px solid #2ecc71;
}

li.minus {
  border-right: 5px solid #c0392b;
}

.delete-btn {
  cursor: pointer;
  background-color: #e74c3c;
  border: 0;
  color: #fff;
  font-size: 20px;
  line-height: 20px;
  padding: 2px 5px;
  position: absolute;
  top: 50%;
  left: 0;
  transform: translate(-100%, -50%);
  opacity: 1;
  transition: opacity 0.3s ease;
}
</style>
