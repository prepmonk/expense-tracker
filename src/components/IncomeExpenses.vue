<template>
  <div class="w-75">
    <div
      class="card rounded-1 shadow d-flex flex-row justify-content-around align-items-center mb-3 p-2">
      <div class="text-center pe-2">
        <h5>Income</h5>
        <p id="money-plus" class="text-success">+${{ income }}</p>
      </div>
      <div class="vr"></div>
      <div class="text-center mx-2">
        <h5>Expense</h5>
        <p id="money-minus" class="text-danger">-${{ expenses * -1 }}</p>
      </div>
    </div>
  </div>
</template>
<script setup>
const props = defineProps({
  income: {
    type: Number,
    required: true,
  },
  expenses: {
    type: Number,
    required: true,
  },
});
</script>

<style scoped>
/* div.card {
  background-color: #fff;
  max-height: 10%;
  min-width: 75%;
}
div.border-end {
  border-right: #dedede;
} */
</style>
