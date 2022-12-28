<template>
  <div class="bg-white">
    <div class="flex justify-center">
        <div class="w-[800px]">
            <div>
                <div class="border-b">
                    <div class="my-4 px-6">
                        <h2 class="font-semibold text-2xl">Expense Tracker</h2>
                    </div>
                </div>
                <div class="px-8 py-2">
                    <h4 class="text-lg text-gray-500 font-thin">Your Balance</h4>
                    <h4 class="text-2xl font-semibold">{{ balance }} tk</h4>
                </div>
                <IncomeExpense :income="income" :expense="expense" />
            </div>
            <div class="flex justify-center">
              <Form class="w-[400px]" @addTransaction="addTransaction" />
              <Transaction class="w-[400px]" @delete="deleteHandler" :transactions="transactions" />
            </div>
        </div>
    </div>
    <p class="text-center text-gray-700 text-xl">&copy; Rasel Ahmed</p>
</div>




  
</template>
<script>
import Transaction from './components/Transaction.vue';
import Form   from './components/Form.vue';
import IncomeExpense from './components/IncomeExpense.vue'
import { computed } from '@vue/runtime-core';

export default {
  name: 'App',
  components: {
    Transaction,Form,IncomeExpense
  },
  data() {
    return {
      transactions: [],
    }
  },
  methods:{
   async deleteHandler(id) {
      const res = await fetch(`api/transactions/${id}`, {
        method:"DELETE",
      });

      res.status == 200 ?
        this.transactions = this.transactions.filter(transaction => transaction.id !== id) :
        alert("There was an error!");
    },
    async addTransaction(transaction) {
      const res = await fetch('api/transactions', {
        method: 'POST',
        body: JSON.stringify(transaction),
        headers: {
          'Content-Type': 'application/json',
          // 'Content-Type': 'application/x-www-form-urlencoded',
        },
      })

      const data = await res.json()
      this.transactions = [{...data},...this.transactions]
    },
    async fetchTransaction() {
      const res = await fetch("api/transactions?_sort=id&_order=desc");

      const data = await res.json();

      return data;
    }
  },
  async created() {
    this.transactions = await this.fetchTransaction()
  },
  computed:{
    income(){
      return this.transactions.reduce((prev , current)=>{
          return current.type == 'income' ? Number(prev) + Number(current.amount) : Number(prev) + 0;
      },0);
    },
    expense(){
      return this.transactions.reduce((prev , current)=>{
          return current.type == 'expense' ? Number(prev) + Number(current.amount) : Number(prev) + 0;
      },0);
    },
    balance(){
        return this.income - this.expense;
    }
  },
}
</script>

<style>

</style>
