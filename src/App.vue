<template>
    <div>
      <Header />
      <div class="container">
        <Balance :total="total" />
        <Expenses :income="income" :expenses="expenses" />
        <Transactions :transactions="transactions" @transactionDeleted="handleTransactionDeleted" />
        <Add @transactionSubmitted="handleTransactionSubmitted" />
      </div>
    </div>
  </template>
  
  <script setup>
  import Header from './components/Header.vue';
  import Balance from './components/Balance.vue';
  import Expenses from './components/Expenses.vue';
  import Transactions from './components/Transactions.vue';
  import Add from './components/Add.vue';
  
  import { toastInjectionKey, useToast } from 'vue-toastification';
  
  import { ref, computed, onMounted } from 'vue';
  
  const transactions = ref([]);

  onMounted(() => {
    const savedTransactions = JSON.parse(localStorage.getItem('transactions'));

    if (savedTransactions) {
      transactions.value = savedTransactions;
    }
  });
  
  // Total
  const total = computed(() => {
    return transactions.value
      .reduce((acc, transaction) => {
        return acc + transaction.amount;
      }, 0)
      .toFixed(2);
  });
  
  // Income
  const income = computed(() => {
    return transactions.value.reduce((acc, transaction) => {
      return transaction.amount > 0 ? acc + transaction.amount : acc;
    }, 0);
  });
  
  // Expenses
  const expenses = computed(() => {
    return transactions.value
      .filter(transaction => transaction.amount < 0)
      .reduce((acc, transaction) => {
        return acc + transaction.amount;
      }, 0);
  });
  
  // Handle Transaction Submitted
  const handleTransactionSubmitted = (transactionData) => {
    const { name, amount, transactionType } = transactionData;
  
    const signedAmount = transactionType === 'expense' ? -Math.abs(amount) : Math.abs(amount);
  
    transactions.value.push({
      id: generateUniqueId(),
      name,
      amount: signedAmount,
    });

    saveTransactionsToLocalStorage();
  
    toast.success('Transaction Submitted');
  };
  
  // Generate Unique Id
  const generateUniqueId = () => {
    return Math.floor(Math.random() * 1000000000);
  };
  
  const toast = useToast();

  // Handle Transaction Deleted
  const handleTransactionDeleted = (id) => {
   transactions.value = transactions.value.filter((transaction) => transaction.id !== id);

   saveTransactionsToLocalStorage();

   toast.success('Transaction Deleted');
  };
  

  // Local Storage
  const saveTransactionsToLocalStorage = () => {
    localStorage.setItem('transactions', JSON.stringify(transactions.value));
  }

  </script>
  
  
  
  
