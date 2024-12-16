<script setup lang="ts">
// Models
const title = defineModel<string>("title");
const amount = defineModel<string>("amount");

// Props
defineProps<{
  addTransaction: () => void;
}>();
</script>

<template>
  <div>
    <h3>Add New Transaction</h3>
    <form @submit.prevent="addTransaction">
      <div>
        <label htmlFor="text">Text</label>
        <input v-model="title" type="text" placeholder="Enter text..." required />
      </div>
      <div>
        <label htmlFor="amount">
          Amount <br />
          (Negative - Expense / Positive - Income)
        </label>
        <input v-model="amount" type="number" step="0.01" placeholder="Enter amount..." required />
      </div>
      <button type="submit" class="btn">Add Transaction</button>
    </form>
  </div>
</template>

<style scoped>
label {
  display: inline-block;
  margin: 10px 0;
}

input[type="text"],
input[type="number"] {
  border: 1px solid #dedede;
  border-radius: 2px;
  display: block;
  font-size: 16px;
  padding: 10px;
  width: 100%;
}

.btn {
  cursor: pointer;
  background-color: #9c88ff;
  box-shadow: var(--box-shadow);
  color: #fff;
  border: 0;
  display: block;
  font-size: 16px;
  margin: 10px 0 30px;
  padding: 10px;
  width: 100%;
}

.btn:focus,
.delete-btn:focus {
  outline: 0;
}
</style>
