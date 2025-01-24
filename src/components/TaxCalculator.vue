<script setup>
import { ref, computed } from 'vue'

const amount = ref(0)
const taxRate = ref(10)
const taxRates = [5, 10, 15, 20]

const calculatedTax = computed(() => (amount.value * taxRate.value) / 100)
const totalAmount = computed(() => amount.value + calculatedTax.value)

const validateAmount = () => {
  if (amount.value < 0) amount.value = 0
}

const formattedTax = computed(() => calculatedTax.value.toFixed(2))
const formattedTotalAmount = computed(() => totalAmount.value.toFixed(2))
</script>

<template>
  <div class="tax-calculator">
    <h1>Tax Calculator</h1>

    <div>
      <label for="amount">Amount:</label>
      <input
        type="number"
        v-model="amount"
        id="amount"
        placeholder="Enter amount"
        @input="validateAmount"
      />
    </div>

    <div>
      <label for="taxRate">Tax Rate (%):</label>
      <select v-model="taxRate" id="taxRate">
        <option v-for="rate in taxRates" :key="rate" :value="rate">{{ rate }}</option>
      </select>
    </div>

    <div class="results">
      <p>Calculated Tax: {{ formattedTax }}</p>
      <p>Total Amount: {{ formattedTotalAmount }}</p>
    </div>
  </div>
</template>

<style scoped>
.tax-calculator {
  font-family: Arial, sans-serif;
  max-width: 400px;
  margin: 20px auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  background: #f9f9f9;
}
label {
  display: block;
  margin-top: 10px;
}
input,
select {
  width: 100%;
  padding: 8px;
  margin-top: 5px;
  margin-bottom: 15px;
  border: 1px solid #ccc;
  border-radius: 4px;
}
.results p {
  font-size: 1.1rem;
  margin: 5px 0;
}
</style>
