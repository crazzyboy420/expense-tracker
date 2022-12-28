<template>
  <div class="px-8 my-6">
    <div class="my-4 border-b w-full">
        <h2 class="font-semibold text-lg">Add new transaction</h2>
    </div>
    <div class="bg-white p-4 border-2 rounded-md">
        <form @submit="onSumit"  class="mt-4">
            <div class="my-5 text-sm">
                <label htmlFor="text" class="block text-black">Text</label>
                <input type="text" autoFocus 
                class="rounded-sm px-4 py-3 mt-1 focus:outline-none bg-gray-100 w-full" 
                placeholder="Enter Text" v-model="text" />
            </div>
            <div class="form-group radio">
              <label for="transaction_type">Type</label>
              <div class="radio_group">
                <input value="income" v-model="type" type="radio" @click="check1" v-bind:checked="condition1" name="transaction_type">
                <label for="transaction_type">Income</label>
              </div>
              <div class="radio_group">
                <input value="expense" v-model="type" type="radio" @click="check2" v-bind:checked="condition2"  name="transaction_type" placeholder="Expense">
                <label for="transaction_type">Expense</label>
              </div>
            </div>
            <div class="my-5 text-sm">
                <label htmlFor="amount" class="block text-black">Amount</label>
                <input v-model="amount" type="number" autoFocus
                class="rounded-sm px-4 py-3 mt-1 focus:outline-none bg-gray-100 w-full" 
                placeholder="Enter Amount" />
            </div>
            <div class="my-5">
                <button class="rounded-sm block text-center text-white bg-gray-800 p-3 duration-300  hover:bg-black w-full">
                    Add Transaction
                </button>
            </div>
        </form>
    </div>
</div>
</template>

<script>
export default {
    name: "Form",
    data(){
      return{
        text:'',
        type:'',
        amount: '',
        condition1: false,
        condition2: false,
      }
    },
  methods: {
      check1() {
      this.condition1 = !this.condition1
      this.condition2 = false
      },
      check2() {
        this.condition2 = !this.condition2
        this.condition1 = false
      },
      onSumit(e){
        e.preventDefault();
        if ((this.text.length < 1) || (this.type.length < 1) || (this.amount < 1)) {
          return alert('Please full fill this form!');
        }
        this.$emit('addTransaction', { title: this.text, type: this.type, amount: this.amount });

        this.text = '';
        this.text = '';
        this.amount = '';
        this.condition1 = false;
        this.condition2 = false;

      }
    }
}
</script>
