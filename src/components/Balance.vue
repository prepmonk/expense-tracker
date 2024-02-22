<template>
  <div class="bg-light-subtle w-75 mb-2">
    <h4 class="fw-medium">Your Balance</h4>
    <h1 id="balance">${{ balance }}</h1>
  </div>
</template>
<script setup>
const props = defineProps({
  balance: {
    type: Number,
    required: true,
  },
});
</script>
