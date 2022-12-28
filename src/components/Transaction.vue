<template>
  <div class="px-8 my-6">
    <div class="my-4 border-b w-full">
        <h2 class="font-semibold text-lg">History</h2>
    </div>
    <div class="overflow-auto max-h-80">
      <TransactionItem v-for="transaction in transactions" @delete="$emit('delete',transaction.id)" :key="transaction.id" :transaction="transaction"  />
    </div>
  </div>
</template>

<script>
import TransactionItem from '../components/TransactionItem.vue'
export default {
    name: "Transaction",
    components:{
      TransactionItem
    },
    emits:['delete'],
    props:['transactions'],
}
</script>

<style scoped>

</style>