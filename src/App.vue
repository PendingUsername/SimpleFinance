<template>
    <Header />
    <div class="container">
        <Balance />
        <Expenses />
        <Transactions />
        <add/>
    </div>
</template>

<script>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue'
import Expenses from './components/Expenses.vue';
import Transactions from './components/Transactions.vue';
import Add from './components/Add.vue';

export default {
    components: {
        Header,
        Balance,
        Expenses,
        Transactions,
        Add,
    },

};
</script>
