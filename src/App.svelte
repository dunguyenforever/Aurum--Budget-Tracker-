<script>
  import SpendingCategory from "./lib/SpendingCategory.svelte";
  import CashflowMonth from "./lib/CashflowMonth.svelte";
  import TotalAssets from "./lib/TotalAssets.svelte";
  import UpcomingTransactions from "./lib/UpcomingTransactions.svelte";
  import RemainingBudgets from "./lib/RemainingBudgets.svelte";
  import TransactionHistory from "./lib/TransactionHistory.svelte";
  import { Col, Container, Row } from "@sveltestrap/sveltestrap";
  import UserInfo from "./lib/UserInfo.svelte";

  let userName = "Du Nguyen";
  let startDate = new Date("2024-09-01");

  let spendingCategory = "";
  let income = 0,
    expenses = 0;
  let upcomingTransactions = "";
  let cash = 0,
    investments = 0,
    properties = 0;
  let transactionHistory = "";
  let remainingBudgets = "";
</script>

<svelte:head>
  <link
    rel="stylesheet"
    href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css"
  />
</svelte:head>
<main>
  <!-- <Container>
    <Row>
      <Col>
        <button on:click={createOverview}>Create Overview</button>
      </Col>
      <UserInfo bind:userName bind:startDate />
    </Row>
  </Container> -->

  <Container>
    <Row>
      <UserInfo bind:userName bind:startDate />
    </Row>
  </Container>

  <Container fluid>
    <Row>
      <Col style="margin-left: 10px">
        <Row class="mb-2" style="height: 40%">
          <SpendingCategory bind:spendingCategory />
        </Row>
        <Row style="height: 59%">
          <CashflowMonth bind:income bind:expenses />
        </Row>
      </Col>

      <Col style="margin-right: 10px; margin-left: 10px; height: 100%">
        <Row class="mb-2">
          <TotalAssets bind:cash bind:investments bind:properties />
        </Row>
        <Row class="mb-2">
          <UpcomingTransactions bind:upcomingTransactions />
        </Row>
        <Row>
          <RemainingBudgets bind:remainingBudgets />
        </Row>
      </Col>

      <Col style="margin-right: 10px">
        <Row style="height: 100%">
          <TransactionHistory bind:transactionHistory />
        </Row>
      </Col>
    </Row>
  </Container>
</main>

<style>
</style>
