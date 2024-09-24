<script>
    let budgets = [];
    let newBudgetName = "";
    let newBudgetAmount = 0;
    let selectedBudget = "";
    let selectedAmount = 0;

    function addBudget() {
        if (newBudgetName && newBudgetAmount > 0) {
            budgets = [...budgets, { name: newBudgetName, amount: newBudgetAmount, originalAmount: newBudgetAmount }];
            newBudgetName = "";  
            newBudgetAmount = 0; 
        }
    }

    function adjustBudget() {
        let index = budgets.findIndex(budget => budget.name === selectedBudget);
        if (index !== -1) {
            budgets[index].amount = selectedAmount;
        }
    }

    $: if (selectedBudget) {
        const budget = budgets.find(b => b.name === selectedBudget);
        if (budget) {
            selectedAmount = budget.amount; 
        }
    }
</script>

<div class="box">
    <h2>Remaining Budgets</h2>

    <input
        type="text"
        placeholder="Enter budget name"
        bind:value={newBudgetName}
    />
    <input
        type="number"
        placeholder="Enter initial budget amount"
        bind:value={newBudgetAmount}
    />
    <button on:click={addBudget}>Add Budget</button>

    {#if budgets.length > 0}
        <div class="budget-control">
            <label for="budgets">Select Budget:</label>
            <select bind:value={selectedBudget}>
                <option value="" disabled selected>Select a budget</option>
                {#each budgets as budget}
                    <option value={budget.name}>{budget.name}</option>
                {/each}
            </select>

   
            {#if selectedBudget}
                <p>Adjust {selectedBudget} Budget:</p>
                <input
                    type="range"
                    min="0"
                    max="100"
                    bind:value={selectedAmount}
                    on:input={adjustBudget}
                />
                <p>Adjusted Amount: ${selectedAmount}</p>
            {/if}
        </div>
    {/if}


    <table>
        <thead>
            <tr>
                <th>Budget Name</th>
                <th>Remaining Amount</th>
            </tr>
        </thead>
        <tbody>
            {#each budgets as budget}
                <tr>
                    <td>{budget.name}</td>
                    <td>${budget.amount}</td>
                </tr>
            {/each}
        </tbody>
    </table>
</div>

<style>
    .box {
        display: flex;
        flex-direction: column;
        justify-content: center;
        padding: 1em;
        border: 1px solid #ccc;
        border-radius: 5px;
        height: auto;
        background-color: #E6E6FA;
        border: 3px solid #A24C76;
    }

    input[type="text"],
    input[type="number"] {
        width: 100%;
        padding: 0.5em;
        margin-top: 0.5em;
        box-sizing: border-box;
        background-color: #F5EAF7;
    }

    input[type="range"] {
        width: 100%;
    }

    h2 {
        margin-bottom: 1rem;
        color: #66023c;
    }

    table {
        width: 100%;
        margin-top: 1rem;
        border-collapse: collapse;
    }

    th, td {
        padding: 0.5em;
        border: 1px solid #ccc;
        text-align: left;
    }

    button {
        margin-top: 0.5em;
        padding: 0.5em;
        background-color: #A24C76;
        color: white;
        border: none;
        border-radius: 5px;
        cursor: pointer;
    }

    button:hover {
        background-color: #7a3258;
    }

    .budget-control {
        margin-top: 1em;
    }

    .box p {
        margin: 0.5em 0;
    }
    select {
        padding: 0.5em;
        margin-top: 0.5em;
        box-sizing: border-box;
        background-color: #f5eaf7;
        color: black;
    }
</style>