<template>
    <div>
        <h4 style="color: #2ecc71; font-size: 1.5em; text-align: center;">Account Balance</h4>
        <h1 id="balance" style="color: #3498db; font-size: 3em; text-align: center; margin-top: 0; margin-bottom: 20px;">${{ total }}</h1>
    </div>
</template>

<script setup>
const props = defineProps({
    total: {
        type: Number,
        required: true,
    },
});
</script>

