<script>
  import { onMount } from "svelte";

  let transactionHistory = {};
  let selectedDate = new Date().toISOString().split('T')[0]; 
  let transactions = [];
  let totalIncome = 0;
  let totalExpense = 0;

  let curTransactions =[];
  
  let amount = '';
  let transactionType = 'income';
  let category = '';
  

  let incomeCategories = [];
  let expenseCategories = [];


  async function fetchTransactionHistory() {
    const response = await fetch('/transactionHistory.json');
    const data = await response.json();
    transactionHistory = data;

    loadTransactionsForDay(selectedDate);
  }
  
  async function fetchCategories() {
    const response = await fetch('/categories.json');
    const data = await response.json();
    incomeCategories = data.incomeCategories;
    expenseCategories = data.expenseCategories;
  }

  function loadTransactionsForDay(date) {
    transactions = transactionHistory[date] || [];
    curTransactions = [...transactions];
    updateTotals();
  }

  function updateTotals() {
    totalIncome = 0;
    totalExpense = 0;
    curTransactions.forEach(transaction => {
      if (transaction.type === "Income") {
        totalIncome += transaction.amount;
      } else if (transaction.type === "Expense") {
        totalExpense += transaction.amount;
      }
    });
  }

  function changeDay(direction) {
    const currentDate = new Date(selectedDate);
    currentDate.setDate(currentDate.getDate() + direction); 
    selectedDate = currentDate.toISOString().split('T')[0];
    loadTransactionsForDay(selectedDate);
  }

  function addTransaction() {
    if (!amount || !category) return;

    const newTransaction = {
      type: transactionType.charAt(0).toUpperCase() + transactionType.slice(1),
      amount: parseFloat(amount),
      category,
      time: new Date().toISOString()
    };
    curTransactions = [newTransaction, ...curTransactions];
    
    updateTotals();
    amount = '';
    category = '';
  }


  onMount(() => {
    fetchTransactionHistory();
    fetchCategories();
  });
</script>

<div class="box">
  <h2>Transaction History</h2>

  <input type="number" bind:value={amount} placeholder="Enter amount" />

  <select bind:value={transactionType}>
    <option value="income">Income</option>
    <option value="expense">Expense</option>
  </select>

  {#if transactionType === 'income'}
    <select bind:value={category}>
      <option value="" disabled selected>Select income category</option>
      {#each incomeCategories as categoryOption}
        <option value={categoryOption}>{categoryOption}</option>
      {/each}
    </select>
  {:else}
    <select bind:value={category}>
      <option value="" disabled selected>Select expense category</option>
      {#each expenseCategories as categoryOption}
        <option value={categoryOption}>{categoryOption}</option>
      {/each}
    </select>
  {/if}

  <button on:click={addTransaction}>Add Transaction</button>

  <div class="date-navigation">
    <button on:click={() => changeDay(-1)}>Previous Day</button>
    <span>{selectedDate}</span>
    <button on:click={() => changeDay(1)}>Next Day</button>
  </div>

  <table>
    <thead>
      <tr>
        <th>Type</th>
        <th>Amount</th>
        <th>Category</th>
        <th>Time</th>
      </tr>
    </thead>
    <tbody>
      {#each curTransactions as transaction}
        <tr>
          <td>{transaction.type}</td>
          <td>{transaction.amount}</td>
          <td>{transaction.category}</td>
          <td>{new Date(transaction.time).toLocaleString()}</td>
        </tr>
      {/each}
    </tbody>
  </table>

  <div class="totals">
    <p><strong>Total Income:</strong> ${totalIncome}</p>
    <p><strong>Total Expense:</strong> ${totalExpense}</p>
  </div>
</div>

<style>
  .box {
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 1em;
    border: 3px solid #a24c76;
    border-radius: 5px;
    height: auto;
    background-color: #e6e6fa;
  }

  .date-navigation {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 1em;
  }

  input, select {
    margin-top: 1em;
    padding: 0.5em;
    width: 100%;
    width: 100%;

    box-sizing: border-box;
    background-color: #f5eaf7;
    color: black;
  }

  button {
    margin-top: 1em;
    padding: 0.5em;
    background-color: #a24c76;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }

  button:hover {
    background-color: #7a3258;
  }

  table {
    width: 100%;
    margin-top: 1em;
    border-collapse: collapse;
  }

  table, th, td {
    border: 1px solid #ccc;
  }

  th, td {
    padding: 0.5em;
    text-align: left;
  }

  .totals {
    margin-top: 1em;
  }

  .totals p {
    font-weight: bold;
  }
</style>
