<template>
  <div class="w-75">
    <h4>Add Transactions</h4>
    <hr />
    <div class="mb-3">
      <label class="form-label" for="text">Text</label>
      <input
        type="text"
        class="form-control"
        placeholder="Enter Text"
        v-model="description" />
    </div>
    <div class="mb-3">
      <label for="amount" class="form-label">Amount</label>
      <p class="form-text mb-2">(negative - expenses, positive - income)</p>

      <input
        class="form-control"
        name="amount"
        type="number"
        v-model="amount"
        placeholder="Enter amount" />
    </div>
    <div class="d-grid">
      <button class="btn btn-purple" @click.prevent="addTransaction">
        Add Transaction
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useToast } from 'vue-toastification';
const emit = defineEmits(['add']);
const toast = useToast();
const description = ref('');
const amount = ref('');
function addTransaction() {
  if (description.value == '' || amount.value == '') {
    toast.error('Both fields must be filled');
    return;
  }
  const data = {
    id: new Date().toISOString(),
    amount: parseFloat(amount.value),
    description: description.value,
  };
  emit('add', data);
  description.value = '';
  amount.value = '';
}
</script>

<style scoped>
.btn-purple {
  background-color: #9c88ff;
  color: white;
}
</style>
