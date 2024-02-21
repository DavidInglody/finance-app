<template>
  <div
    class="grid grid-cols-2 py-4 border-b border-gray-200 dark:border-gray-400 text-gray-500 dark:text-gray-100"
  >
    <div class="flex items-center justify-between">
      {{ date }}
    </div>
    <div class="flex items-center justify-end">{{ currency }}</div>
  </div>
</template>

<script setup>
const props = defineProps({
  date: String,
  transaction: Object,
});

const sum = computed(() => {
  let sum = 0;

  for (const transaction of props.transaction) {
    if (transaction.type === "Income") {
      sum += transaction.amount;
    } else {
      sum -= transaction.amount;
    }
  }
  return sum;
});

const { currency } = useCurrency(sum);
</script>
