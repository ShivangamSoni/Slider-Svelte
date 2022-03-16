<script>
  let info_sign_src = "../Assets/sign.svg";

  export let cost;
  let previousCost = cost;
  const costUpdate = (node, value) => {
    return {
      update(value) {
        value = parseInt(value);
        cost = Number.isNaN(value) ? previousCost : value;
        previousCost = cost;
        calculateTip();
      },
    };
  };

  export let tip;
  $: tipValue = (cost / 100) * tip;
  // For Positioning of Range Fill & Tooltip Position
  $: tip_fill = (tip / 5) * (100 / 6);

  let sliderSections = [1, 2, 3, 4, 5];
</script>

<div class="container">
  <div class="amount">
    <label for="amount-input">Enter your donation</label>
    <div class="input-area">
      <div class="currency"><span class="currency-sign">$</span> <span class="currency-abbr">USD</span></div>
      <input type="text" id="amount-input" bind:value={cost} use:costUpdate={cost} />
      <div class="leading-zero">.00</div>
    </div>
  </div>

  <div class="tip">
    <h1>Tip GoFundMe Service</h1>
    <p class="text-light">GoFundMe has a 0% platform fee for organizers. GoFundMe will continue offering its services thanks to donors who will leave an optional amount here:</p>
  </div>

  <div class="tip-slider">
    <div class="slider">
      <div class="text-light">0%</div>
      <div class="slider-input">
        <input type="range" min="0" max="30" step="5" bind:value={tip} />

        <div class="slider-sections">
          {#each sliderSections as section (section)}
            <span />
          {/each}
        </div>

        <div class="slider-fill" style={`width: ${tip_fill}%`} />

        <div class="slider-tooltip">
          <span class="tooltip" style={`left: ${tip_fill}%`}>
            {#if tipValue > 0}
              <span>${tipValue}</span>&nbsp;
            {/if}
            ({tip}%)</span
          >
        </div>
      </div>
      <div class="text-light">30%</div>
    </div>

    {#if tip == 0 && cost > 0}
      <div class="slider-info">
        <div class="info-img">
          <img src={info_sign_src} alt="info" />
        </div>
        <div>Adding a GoFundMe tip means being a key part of improving the services for donors like you and the campaigns you support.</div>
      </div>
    {/if}
  </div>
</div>

<style>
  .container {
    display: flex;
    flex-direction: column;
    row-gap: 1rem;
  }

  .amount {
    display: flex;
    flex-flow: column nowrap;
  }

  .amount > label {
    font-size: 1rem;
    font-weight: 900;
    cursor: pointer;
  }

  .input-area {
    display: flex;
    align-items: center;
    justify-content: space-between;
    border: 1px solid #c8c8c8;
    border-radius: 5px;
    font-weight: 900;
    padding: 0.7rem 1rem;
  }

  .input-area:focus-within {
    outline: 1px auto #90ceff;
    outline: 5px auto -webkit-focus-ring-color;
  }

  .input-area > input {
    appearance: none;
    border: none;
    outline: none;
    display: block;
    width: 100%;
    font-size: 2.5rem;
    font-weight: 900;
    text-align: right;
    align-self: baseline;
    height: 100%;
  }

  .leading-zero {
    font-size: 2.5rem;
    align-self: baseline;
  }

  .currency {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .currency-sign {
    font-size: 1.5rem;
  }

  .currency-abbr {
    font-size: 0.875rem;
  }

  .tip > h1 {
    font-weight: 600;
  }

  .tip > p {
    font-size: 0.875rem;
  }

  .slider {
    display: flex;
    align-items: baseline;
    justify-content: space-evenly;
    padding-top: 4rem;
  }

  .slider-input {
    flex-grow: 1;
    margin: 0 0.5rem;
    position: relative;
  }

  .slider-input > input {
    appearance: none;
    background-color: #c8c8c8;
    display: block;
    width: 100%;
    position: absolute;
    top: 0;
    left: 0;
    margin: 0;
    padding: 0;
    height: 0.5rem;
    border: none;
    border-radius: 0.25rem;
    font-size: 1rem;
  }

  .slider-input > input::-webkit-slider-thumb {
    appearance: none;
    width: 1.5rem;
    height: 1.5rem;
    border: 3px solid #fff;
    border-radius: 50%;
    background: #02a95c;
    position: relative;
    z-index: 2;
    cursor: pointer;
  }

  .slider-sections {
    width: 100%;
    height: 0.5rem;
    margin: 0;
    padding: 0;
    display: flex;
    align-items: center;
    justify-content: space-evenly;
    border-radius: 0.25rem;
  }

  .slider-sections > span {
    width: 3px;
    height: 100%;
    background-color: #fff;
    z-index: 1;
  }

  .slider-fill {
    background-color: #9addbe;
    position: absolute;
    top: 0;
    left: 0;
    pointer-events: none;
    border-radius: 0.25rem;
    height: 0.5rem;
  }

  .slider-tooltip {
    position: relative;
    top: -4rem;
    left: 0;
    width: 100%;
  }

  .tooltip {
    position: absolute;
    top: 0;
    left: 0;
    transform: translateX(-50%);
    background-color: #fff;
    border-radius: 0.25rem;
    box-shadow: 0 2px 6px rgb(0 0 0 / 10%);
    padding: 0.5rem;
    text-align: center;
    width: fit-content;
  }

  .tooltip > span {
    font-weight: 900;
  }

  .slider-info {
    font-size: 0.875rem;
    padding: 1rem;
    display: grid;
    grid-template-columns: 1fr 9fr;
    column-gap: 10px;
    align-items: center;
  }
</style>
