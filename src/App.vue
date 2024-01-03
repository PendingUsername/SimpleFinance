<template>
    <Header />
    <div class="container">
        <Balance />
        <Expenses />
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

import { ref } from 'vue';

const transactions = ref([
          { id: 1, name: 'Cash', amount: -400 },
          { id: 2, name: 'Paycheck', amount: 800 },
          { id: 3, name: 'Computer', amount: -800 },
          { id: 4, name: 'Paycheck', amount: 800 },
]);
</script>
