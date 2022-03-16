<script>
  export let cost;
  export let tip;

  $: tipValue = (cost / 100) * tip;
</script>

<div class="container">
  <h1>Your Donation</h1>
  <div class="text-light"><span>Your donation</span> <span>${cost}</span></div>
  <div class="text-light"><span>GoFundMe tip</span> <span>${tipValue}</span></div>
  <div class="total"><span>Total due Today</span> <span>${cost + tipValue}</span></div>
</div>

<style>
  .container {
    display: flex;
    flex-direction: column;
    row-gap: 10px;
    font-size: 0.875rem;
  }
  h1 {
    font-weight: 900;
  }

  .container > div {
    display: flex;
    align-items: baseline;
    justify-content: space-between;
  }

  .total {
    margin-top: 10px;
    border-top: 2px solid #333;
  }
</style>
