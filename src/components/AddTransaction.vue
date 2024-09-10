<template>
    <h3>Add Transaction</h3>
    <form id ="form" @submit.prevent="onSubmit">
        <div class="form-control">
            <label for="text">Text</label>
            <input type="text" id="text" v-model="text" placeholder="Enter text...">
        </div>
        <div class="form-control">
            <label for="amount"
                >Amount <br />
                (negative - expense, positive - income)</label
            >
            <input type="number" id="amount" v-model="amount" placeholder="Enter amount...">
        </div>
        <button class="btn">Add transaction</button>
    </form>
</template>

<script setup>
import { useToast } from 'vue-toastification';
import { ref } from 'vue';


const text = ref('');
const amount = ref('');

const toast = useToast();

const emit = defineEmits(['add-transaction']);

const onSubmit = () => {
  if (!text.value || !amount.value) {
    // Display a toast error message if either field is empty
    toast.error('Both fields must be filled.');
    return;
  }

  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value),
  };

  emit('transactionSubmitted', transactionData);

  // Clear form fields
  text.value = '';
  amount.value = '';
};

</script>