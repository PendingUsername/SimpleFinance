<template>
    <div>
        <h3 class="section-heading">Add Transaction</h3>
        <form id="transaction-form" @submit.prevent="addTransaction" class="form">
            <div class="form-control">
                <label for="text" class="label">Text</label>
                <input v-model="text" type="text" id="text" placeholder="Enter text here." required class="input">
            </div>
            <div class="form-control">
                <label for="transaction-type" class="label">Transaction Type</label>
                <select v-model="transactionType" id="transaction-type" class="select">
                    <option value="income">Income</option>
                    <option value="expense">Expense</option>
                </select>
            </div>
            <div class="form-control">
                <label for="amount" class="label">Amount</label>
                <input v-model="amount" type="text" id="amount" placeholder="Enter amount here." required class="input">
            </div>
            <button type="submit" class="btn btn-primary">Add Transaction</button>
        </form>
    </div>
</template>

<script>
export default {
    data() {
        return {
            text: "",
            transactionType: "income",
            amount: ""
        };
    },
    methods: {
        addTransaction() {
            // Validate input
            if (!this.text.trim() || !this.amount.trim()) {
                alert("Please enter both text and amount.");
                return;
            }

            // Convert amount to number
            const numericAmount = parseFloat(this.amount);

            // Validate numericAmount
            if (isNaN(numericAmount)) {
                alert("Please enter a valid numeric amount.");
                return;
            }

            // Adjust amount based on transaction type
            const adjustedAmount = this.transactionType === "expense" ? -numericAmount : numericAmount;

            // Emit an event or call a method to add the transaction with this.text and adjustedAmount
            // Example: this.$emit("add-transaction", { text: this.text, amount: adjustedAmount });

            // Clear the input fields after adding the transaction
            this.text = "";
            this.transactionType = "income";
            this.amount = "";
        }
    }
};
</script>

<style>
.section-heading {
    color: #3498db;
    text-align: center;
}

.form {
    max-width: 400px;
    margin: 0 auto;
}

.form-control {
    margin-bottom: 15px;
}

.label {
    display: block;
    margin-bottom: 5px;
    color: #3498db;
}

.input, .select {
    width: 100%;
    padding: 8px;
    box-sizing: border-box;
}

.btn-primary {
    background-color: #3498db;
    color: white;
    border: none;
    padding: 10px;
    border-radius: 5px;
    cursor: pointer;
}

.btn-primary:hover {
    background-color: #2980b9;
}
</style>



