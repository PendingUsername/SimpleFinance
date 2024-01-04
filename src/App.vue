<template>
    <Header />
    <div class="container">
        <Balance :total="total" />
        <Expenses :income="income" :expenses="expenses" />
        <Transactions :transactions="transactions"  />
        <add/>
    </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import Expenses from './components/Expenses.vue';
import Transactions from './components/Transactions.vue';
import Add from './components/Add.vue';

import { ref, computed } from 'vue';

const transactions = ref([
          { id: 1, name: 'Cash', amount: -400 },
          { id: 2, name: 'Paycheck', amount: 800 },
          { id: 3, name: 'Computer', amount: -800 },
          { id: 4, name: 'Paycheck', amount: 800 },
]);
// Total 
const total = computed(() => {
    return transactions.value
        .filter(transaction => transaction.amount > 0)
        .reduce((acc, transaction) => {
            return acc + transaction.amount;
        }, 0)
        .toFixed(2);
});


// Income
const income = computed(() => {
    return transactions.value.reduce((acc, transaction) => {
        return acc + transaction.amount;
    }, 0);
});

// Expenses
const expenses = computed(() => {
    return transactions.value
        .filter(transaction => transaction.amount < 0)
        .reduce((acc, transaction) => {
            return acc + transaction.amount;
        }, 0)
        .toFixed(2);
});
</script>
