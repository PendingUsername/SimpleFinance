<template>
    <div class="inc-exp-container">
        <div class="income-section">
            <h4>Income</h4>
            <p id="money-plus" class="money plus">${{ income.toFixed(2) }}</p>
        </div>
        <div class="expense-section">
            <h4>Expense</h4>
            <p id="money-minus" class="money minus">${{ Math.abs(expenses).toFixed(2) }}</p>
        </div>
    </div>
</template>


<script setup>
    import { defineProps } from 'vue';

    const props = defineProps({
        income: {
            type: Number,
            required: true,
        },
        expenses: {
            type: Number,
            required: true,
        }
    });
</script>

<style>
.inc-exp-container {
    display: flex;
    justify-content: space-around;
    background-color: #f2f2f2;
    padding: 15px;
    border-radius: 8px;
}

.income-section,
.expense-section {
    text-align: center;
}

.income-section h4,
.expense-section h4 {
    color: #2ecc71;
}

.income-section p,
.expense-section p {
    color: #3498db;
    font-weight: bold;
    font-size: 1.2em;
    margin: 5px 0;
}

.plus {
    color: #2ecc71;
}

.minus {
    color: #e74c3c;
}
</style>
