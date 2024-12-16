<script setup lang="ts">
import { ref, reactive, computed } from "vue";
import { nanoid } from "nanoid";

import TotalBalance from "./components/total-balance.vue";
import IncomeExpenses from "./components/income-expenses.vue";
import TransactionList from "./components/transaction-list.vue";
import AddTransaction from "./components/add-transaction.vue";

import type { Transaction } from "./types/types";

// Transactions state
const transactions = ref<Transaction[]>([]);

// Form state
const formData = reactive({
  title: "",
  amount: "",
});

// Calculate total balance
const total = computed(() =>
  transactions.value.reduce((acc, transaction) => acc + transaction.amount, 0),
);

// Calculate income
const income = computed(() =>
  transactions.value.reduce((acc, transaction) => {
    if (transaction.amount > 0) {
      acc += transaction.amount;
    }
    return acc;
  }, 0),
);

// Calculate expense
const expense = computed(
  () =>
    transactions.value.reduce((acc, transaction) => {
      if (transaction.amount < 0) {
        acc += transaction.amount;
      }
      return acc;
    }, 0) * -1,
);

/** Callback to add a new transaction */
const addTransaction = () => {
  const newTransaction: Transaction = {
    id: nanoid(),
    title: formData.title,
    amount: Number(formData.amount),
  };

  transactions.value.push(newTransaction);
  formData.title = "";
  formData.amount = "";
};

/** Callback to delete a transaction by id */
const deleteTransaction = (id: string) => {
  const transactionIndex = transactions.value.findIndex((transaction) => transaction.id === id);

  if (transactionIndex !== -1) {
    transactions.value.splice(transactionIndex, 1);
  }
};
</script>

<template>
  <div>
    <h2>Expense Tracker</h2>
    <div class="container">
      <TotalBalance :total="total" />
      <IncomeExpenses :income="income" :expense="expense" />
      <TransactionList :transactions="transactions" :handle-delete="deleteTransaction" />
      <AddTransaction
        v-model:title="formData.title"
        v-model:amount="formData.amount"
        :add-transaction="addTransaction"
      />
    </div>
  </div>
</template>

<style>
.container {
  margin: 30px auto;
  width: 300px;
}

@media (max-width: 320px) {
  .container {
    width: 300px;
  }
}
</style>
