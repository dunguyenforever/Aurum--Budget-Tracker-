<!-- TotalAssets.svelte -->
<script>
    export let cash = 0;
    export let investments = 0;
    export let properties = 0;

    function updateAsset(type, e) {
        if (type === 'cash') cash = parseFloat(e.target.value) || 0;
        if (type === 'investments') investments = parseFloat(e.target.value) || 0;
        if (type === 'properties') properties = parseFloat(e.target.value) || 0;
    }
</script>

<div class="box">
    <h2 class='m-0'>Total Assets</h2>
    <p class='m-0'>Cash: {cash}</p>
    <p class='m-0'> Investments: {investments}</p>
    <p>Properties: {properties}</p>
    <input type="number" placeholder="Cash" on:input={e => updateAsset('cash', e)} />
    <input type="number" placeholder="Investments" on:input={e => updateAsset('investments', e)} />
    <input type="number" placeholder="Properties" on:input={e => updateAsset('properties', e)} />
</div>

<style>
    .box {
        display: flex;
        flex-direction: column;
        justify-content: center ;
        padding: 1em;
        border: 1px solid #ccc;
        border-radius: 5px;
        height: 100%;
        border: 3px solid #A24C76;
        background-color: #E6E6FA;
    }

    input {
        width: 100%;
        padding: 0.5em;
        box-sizing: border-box;
        background-color: #F5EAF7;
    }

    h2 {
        margin-bottom: 1rem;
        color: #66023c;
    }
    
</style>
