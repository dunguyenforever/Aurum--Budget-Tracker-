<!-- SpendingCategory.svelte -->
<script>
    import CategoryChart from "./CategoryChart.svelte";

    //export let spendingCategory = "";
</script>

<div class="box">
    <h2>Spending Category</h2>
    <!-- <p>{spendingCategory}</p> -->
    <CategoryChart />
    <!-- <input placeholder="Input expense category" bind:value={spendingCategory} /> -->
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
        border: 3px solid #A24C76;
        background-color: #E6E6FA;
    }
/* 
    input {
        width: 100%;
        padding: 0.5em;
        margin-top: 0.5em;
        box-sizing: border-box;
        background-color:#F5EAF7;
    } */

    h2 {
        margin-bottom: 1rem;
        color: #66023c;
    }
</style>
