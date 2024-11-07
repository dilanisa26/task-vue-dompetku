<script setup>
import { ref } from 'vue'

const entries = ref([]) // Array to store entries
const description = ref('') // Model for "Keterangan" input
const amount = ref('') // Model for "Jumlah Uang" input

// Function to submit a new entry
const submitEntry = () => {
  if (description.value && amount.value) {
    entries.value.push({
      id: Date.now(),
      description: description.value,
      amount: parseFloat(amount.value),
    })
    description.value = ''
    amount.value = ''
  }
}

// Function to delete a specific entry
const deleteEntry = (id) => {
  entries.value = entries.value.filter(entry => entry.id !== id)
}

// Function to delete all entries
const clearAllEntries = () => {
  entries.value = []
}
</script>

<template>
  <div class="arsip-dompetku">
    <h2>Dompetku</h2>
    <div class="input-group">
      <label for="description">Keterangan Transaksi:</label>
      <input id="description" v-model="description" placeholder="Masukkan keterangan" />

      <label for="amount">Jumlah Uang (in/out):</label>
      <input id="amount" v-model="amount" type="number" placeholder="Masukkan jumlah uang" />

      <button @click="submitEntry">Submit</button>
    </div>

    <div v-if="entries.length" class="entry-list">
      <h3>Daftar Transaksi</h3>
      <ul>
        <li v-for="entry in entries" :key="entry.id">
          <span>{{ entry.description }} - Rp{{ entry.amount.toLocaleString() }}</span>
          <button @click="deleteEntry(entry.id)">Delete</button>
        </li>
      </ul>
      <button @click="clearAllEntries" class="clear-button">Delete All</button>
    </div>
    <p v-else>Tidak ada transaksi</p>
  </div>
</template>

<ArsipDompetku style="margin-bottom: 50px;" />

<style scoped>
.large-spacing {
  margin-bottom: 50px; /* Adjust as needed */
}
</style>

<style scoped>
.arsip-dompetku {
  max-width: 600px;
  margin: 20px auto;
  padding: 1.5rem;
  background-color: #f5faff;
  border: 1px solid #d0e4f7;
  border-radius: 12px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

h2 {
  text-align: center;
  font-size: 2rem;
  color: #333;
  margin-bottom: 1rem;
}

.input-group {
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
  margin-bottom: 1.5rem;
}

label {
  font-weight: 600;
  color: #1a1a1a;
}

input {
  padding: 0.6rem;
  border: 1px solid #bcd4e6;
  border-radius: 6px;
  outline: none;
  transition: border 0.3s;
}

input:focus {
  border-color: #3498db;
}

button {
  padding: 0.6rem;
  color: #fff;
  background-color: #3498db;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-weight: bold;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #2980b9;
}

.entry-list {
  margin-top: 1rem;
}

.entry-list h3 {
  text-align: center;
  color: #333;
  margin-bottom: 0.5rem;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.5rem 0;
  border-bottom: 1px solid #ddd;
}

li span {
  color: #555;
}

li button {
  padding: 0.3rem 0.6rem;
  background-color: #e74c3c;
  border: none;
  border-radius: 4px;
  color: #fff;
  cursor: pointer;
  transition: background-color 0.3s;
}

li button:hover {
  background-color: #c0392b;
}

.clear-button {
  width: 100%;
  margin-top: 1rem;
  background-color: #e74c3c;
  color: #fff;
  font-weight: bold;
}

.clear-button:hover {
  background-color: #c0392b;
}
</style>
