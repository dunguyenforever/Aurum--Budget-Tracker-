<script>
    import { onMount } from "svelte";

    let transactions = [];
    let amount = "";
    let transactionType = "income"; 
    let category = "";
    let date = new Date().toISOString().split("T")[0]; 

    let incomeCategories = [];
    let expenseCategories = [];

    async function fetchCategories() {
        const response = await fetch("/categories.json");
        const data = await response.json();
        incomeCategories = data.incomeCategories;
        expenseCategories = data.expenseCategories;
    }

    function addTransaction() {
        if (!amount || !category) return;

        const typeDisplay = transactionType === "income" ? `[Income]` : `[Expense]`;
        const color = transactionType === "income" ? "green" : "red";

        transactions = [
            ...transactions,
            {
                typeDisplay,
                color,
                amount,
                category,
                date: new Date(date).toLocaleDateString(),
            },
        ];

        amount = "";
        category = "";
        date = new Date().toISOString().split("T")[0]; 
    }

    onMount(() => {
        fetchCategories();
    });
</script>

<div class="box">
    <h2>Upcoming Transactions</h2>

    <input type="number" bind:value={amount} placeholder="Enter amount" />

    <select bind:value={transactionType}>
        <option value="income">Income</option>
        <option value="expense">Expense</option>
    </select>

    {#if transactionType === "income"}
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

    <input type="date" bind:value={date} />

    <button on:click={addTransaction}>Add Transaction</button>

    <div class="transaction-list">
        {#each transactions as transaction}
            <p style="color:{transaction.color}">
                {transaction.typeDisplay}, Amount: {transaction.amount}, Category: {transaction.category}, Date: {transaction.date}
            </p>
        {/each}
    </div>
</div>

<style>
    .box {
        display: flex;
        flex-direction: column;
        justify-content: center;
        padding: 1em;
        border: 1px solid #ccc;
        border-radius: 5px;
        height: 100%;
        background-color: #e6e6fa;
        border: 3px solid #a24c76;
    }

    input,
    select {
        width: 100%;
        padding: 0.5em;
        margin-top: 0.5em;
        box-sizing: border-box;
        background-color: #f5eaf7;
        color: black;
    }

    h2 {
        margin-bottom: 1rem;
        color: #66023c;
    }

    .transaction-list {
        margin-top: 1em;
        padding: 0.5em;
        background-color: #f5eaf7;
        border: 1px solid #ccc;
        border-radius: 5px;
        height: auto;
    }

    button {
        padding: 0.5em;
        margin-top: 1em;
        background-color: #a24c76;
        color: white;
        border: none;
        border-radius: 5px;
        cursor: pointer;
    }

    button:hover {
        background-color: #7a3258;
    }

    .transaction-list p {
        margin: 0.5em 0;
    }
</style>
