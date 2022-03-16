<script>
  import Donation from "../Components/Donation.svelte";
  import Summary from "../Components/Summary.svelte";

  let cost = 5;
  let tip = 5;
</script>

<main>
  <Donation bind:cost bind:tip />
  <Summary {cost} {tip} />
</main>

<style>
  main {
    width: 900px;
    max-width: 95%;
    margin: 0 auto;
    display: grid;
    grid-template-columns: minmax(0, 70%) minmax(0, 30%);
    column-gap: 30px;
    align-items: flex-start;
  }
</style>
