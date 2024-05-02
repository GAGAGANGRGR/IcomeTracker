<template>
  <Header :totalIncome="totalIncome()" />
  <Forms :inputData="inputData" @formdata="formdata" />
  <div class="center-table" v-if="formDataArray.length > 0">
      <table>
          <thead>
              <tr>
                  <th>Description</th>
                  <th>Amount</th>
                  <th>Date<span class="light-text"> (yyyy/mm/dd)</span></th>
                  <th>Remove</th>
              </tr>
          </thead>
          <tbody>
              <tr v-for="(income, index) in formDataArray" :key="index">
                  <td class="description-cell">{{ income.desc }}</td>
                  <td class="amount-cell"><span class="light-text">Rs.</span> {{ income.amt }}</td>
                    <td>{{ income.date }} </td>
                  <td><button @click="removeItem(index)" class="delete">Delete</button></td>
              </tr>
          </tbody>
      </table>
  </div>
</template>

<style scoped>
.amount-cell {
    width: 120px; /* Adjust as needed */
}
.light-text {
    color: #999; /* Light gray color */
}
.center-table {
    margin-left: auto;
    margin-right: auto;
    margin-top: 8ch;
}

.center-table table {
    border-collapse: collapse;
    width: 40%;
    margin: auto;
}

.center-table th,
.center-table td {
    border: 1px solid #ddd;
    padding: 8px;
    text-align: left;
}

.delete {
    background-color: #fff;
    border: 1px solid #f00;
    color: #f00;
    padding: 6px 10px;
    border-radius: 4px;
    transition: background-color 0.3s ease, color 0.3s ease;
}

.delete:hover {
    background-color: #f00;
    color: #fff;
}

.delete:focus {
    outline: none;
}

/* Add animation */
@keyframes fadeIn {
    from {
        opacity: 0;
    }
    to {
        opacity: 1;
    }
}

.fade-in {
    animation: fadeIn 0.5s ease;
}
.description-cell {
  width: 40%;
    word-wrap: pre-wrap ; /* or word-break: break-all; */
}
</style>

<script setup>
import { ref } from 'vue';
const formDataArray = ref([]);
const temp=ref(0)
const inputData = ref([
    { type: 'text', placeholder: 'Enter Description', value: '', var: 'desc' },
    { type: 'number', placeholder: 'Enter Amount', value: '', var: 'amt' },
    { type: 'date', placeholder: 'Enter Date', value: '', var: 'date' },
]);

const formdata = (data) => {
    console.log('data', data);
     formDataArray.value.push({...data}); 
    console.log('formDataArray.value',formDataArray.value);
}

const totalIncome = function() {
    return formDataArray.value.reduce((total, income) => total + parseFloat(income.amt), 0);
}

const removeItem = (index) => {
  formDataArray.value.splice(index, 1); // Remove item at the specified index
};  
</script>


