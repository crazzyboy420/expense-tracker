<template>
    <div :class="[transaction.type == 'income'? ' border-green-500':'border-red-500']" class="ml-6 relative bg-white p-4 border-r-8 shadow-md my-4 flex justify-between">
        <div class="absolute -left-6">
            <div @click="$emit('delete',transaction.id)" class="cursor-pointer bg-red-600 p-2 w-6 flex items-center text-xs text-white justify-center">
                x
            </div>
        </div>
        <div>
            <p>{{ transaction.title }}</p>
        </div>
        <div>
            <p>{{ transaction.type== "income" ? '+' : '-' }}{{ transaction.amount }} tk</p>
        </div>
    </div>
</template>

<script>
export default {
    name:"TranctionItem",
    props:['transaction']
}
</script>