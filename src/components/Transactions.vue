<template>
    <div>
      <h3 style="color: #3498db; text-align: center;">Transaction History</h3>
      <ul id="list" class="list">
        <li v-for="transaction in transactions" :key="transaction.id" :class="{ 'transaction': true, 'minus': transaction.amount < 0, 'plus': transaction.amount > 0 }">
          {{ transaction.name }} <span>{{ transaction.amount < 0 ? '-' : '+' }}${{ Math.abs(transaction.amount) }}</span><button @click="deleteTransaction(transaction.id)" class="delete-btn">X</button>
        </li>
      </ul>
    </div>
  </template>

<script setup>
import { defineProps } from 'vue';

const emit = defineEmits(['transactionDeleted']);

const props = defineProps({
    transactions: {
        type: Array,
        required: true
    }
});

const deleteTransaction = (id) => {
    emit('transactionDeleted', id);
};
</script>
  <style>
  .list {
    list-style-type: none;
    padding: 0;
  }
  
  .transaction {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #ecf0f1;
    border-radius: 5px;
    margin: 5px 0;
    padding: 10px;
  }
  
  .transaction.minus {
    border-left: 5px solid #e74c3c;
  }
  
  .transaction.plus {
    border-left: 5px solid #2ecc71;
  }
  
  .transaction span {
    margin-left: auto;
    margin-right: 10px;
    color: #3498db;
    font-weight: bold;
  }
  
  .delete-btn {
    background-color: #e74c3c;
    color: white;
    border: none;
    padding: 5px 10px;
    border-radius: 3px;
    cursor: pointer;
    font-weight: bold;
  }
  
  .delete-btn:hover {
    background-color: #c0392b;
  }
  </style>
  
