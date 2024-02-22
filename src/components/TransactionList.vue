<template>
  <div class="w-75 mb-4">
    <h3>History</h3>
    <hr />

    <ul class="list-group rounded vstack gap-2">
      <li
        v-for="transaction in transactionsList"
        :key="transaction.id"
        class="list-group-item d-flex justify-content-between align-items-center border-0 rounded-1 shadow hstack border-0 border-end border-5 mb-1 ps-2"
        :class="{
          'border-danger': transaction.amount < 0,
          'border-success': transaction.amount >= 0,
        }">
        <button
          @click.prevent="deleteTransaction(transaction.id)"
          class="delete-btn">
          x
        </button>
        <div>{{ transaction.description }}</div>
        <div>
          <span>{{ transaction.amount > 0 ? '' : '-' }}</span>
          <span
            >${{ transaction.amount * (transaction.amount > 0 ? 1 : -1) }}</span
          >
        </div>
      </li>
    </ul>
  </div>
</template>
<script setup>
const props = defineProps({
  transactionsList: Object,
});
const emit = defineEmits(['deleteTransaction']);
const deleteTransaction = transactionId => {
  emit('deleteTransaction', transactionId);
};
</script>

<style scoped>
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
  opacity: 0;
  transition: opacity 0.3s ease;
}

.list-group li:hover .delete-btn {
  opacity: 1;
}
</style>
