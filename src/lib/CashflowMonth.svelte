<!-- CashflowMonth.svelte -->
<script>
    import { Col, Row } from "@sveltestrap/sveltestrap";
    import BarInOutMoney from "./BarInOutMoney.svelte";

    export let income = 0;

    export let expenses = 0;

    function updateIncome(e) {
        income = parseFloat(e.target.value) || 0;
    }

    function updateExpenses(e) {
        expenses = parseFloat(e.target.value) || 0;
    }

</script>

<div class="box">
    <h2>Cashflow of the Month</h2>

    <section class="mb-5">
        <Row>
            <Col>
                <div>Income: {income}</div>
                <input type="number" placeholder="Income" on:input={updateIncome} />
            </Col>
            <Col>
                <div>Expenses: {expenses}</div>
                <input type="number" placeholder="Expenses" on:input={updateExpenses} />
            </Col>
        </Row>
    </section>

    <BarInOutMoney />
    <!-- <div>Income: {income}</div>
    <div>Expenses: {expenses}</div>
    <input type="number" placeholder="Income" on:input={updateIncome} />
     -->

</div>

<style>
    .box {
        display: flex;
        flex-direction: column;
        justify-content: center ;
        padding: 1em;
        border-radius: 5px;
        height: 100%;
        background-color: #E6E6FA;
        border: 3px solid #A24C76;
    }

    input {
        width: 100%;
        padding: 0.5em;
        margin-top: 0.5em;
        box-sizing: border-box;
        background-color: #F5EAF7;
    }

    h2 {
        margin-bottom: 1rem;
        color: #66023c;
    }

</style>
