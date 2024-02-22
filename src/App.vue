<script setup>
import { ref, computed, onMounted } from 'vue';
import { useToast } from 'vue-toastification';
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';
const toast = useToast();
const balance = ref(1000);
const transactionsList = ref([]);
onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'));
  if (savedTransactions) {
    transactionsList.value = savedTransactions;
  }
});
const amount = computed(() => {
  return transactionsList.value
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});
const income = computed(() => {
  return transactionsList.value
    .filter(transaction => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});
const expenses = computed(() => {
  return transactionsList.value
    .filter(transaction => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});
function addTransaction(transaction) {
  balance.value = balance.value + transaction.amount;
  transactionsList.value.push(transaction);
  saveTransactions();
  toast.success('Transaction Added');
}
const deleteTransaction = transactionId => {
  transactionsList.value = transactionsList.value.filter(
    transaction => transaction.id !== transactionId
  );
  saveTransactions();
  toast.success('Transaction deleted');
};
//Save to local storage
const saveTransactions = () => {
  localStorage.setItem('transactions', JSON.stringify(transactionsList.value));
};
</script>
<template>
  <Header />
  <main
    class="container-sm d-flex vh-100 justify-content-center flex-column align-items-center bg-light-subtle">
    <Balance :balance="+amount" />
    <IncomeExpenses :income="+income" :expenses="+expenses" />
    <TransactionList
      :transactionsList="transactionsList"
      @deleteTransaction="deleteTransaction" />
    <AddTransaction @add="addTransaction" />
  </main>
</template>
<style scoped></style>
