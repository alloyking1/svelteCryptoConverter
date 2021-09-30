<script>
  import { fly, fade } from "svelte/transition";
  let hasError = false;
  let isSuccessVisible = false;
  let submitted = false;

  let amount = "";
  let baseCoin;
  let convertCoin;

  const errMessage = "All the fields are mandatory";

  function handleSubmit(e) {
    isSuccessVisible = true;
    conversion(amount, baseCoin, convertCoin);
  }

  function conversion(amount, baseCoin, convertCoin) {
    console.log(baseCoin);
    console.log(convertCoin);
    console.log(amount);
  }
</script>

<h2>Take survey</h2>

{#if hasError == true}
  <p class="error-alert">{errMessage}</p>
{:else if isSuccessVisible}
  <p class="error-alert" transition:fade={{ duration: 150 }}>
    Data updated successfully
  </p>
{/if}

<div class="container">
  <form
    id="surveyForm"
    class="mt-4"
    class:submitted
    on:submit|preventDefault={handleSubmit}
  >
    <div class="form-group">
      <label for="baseCoin">Choose base currency:</label>
      <select name="baseCoin" bind:value={baseCoin}>
        <option value="BTC">Bitcoin</option>
        <option value="ETH">Ethereum</option>
        <option value="fiat">Fiat</option>
        <option value="audi">Audi</option>
      </select>
    </div>

    <div class="form-group">
      <label for="compareCoin">Choose currency to convert to:</label>
      <select name="compareCoin" bind:value={convertCoin}>
        <option value="BTC">Bitcoin</option>
        <option value="ETH">Ethereum</option>
        <option value="fiat">Fiat</option>
        <option value="audi">Audi</option>
      </select>
    </div>

    <div class="form-group">
      <input
        type="num"
        class="form-control"
        placeholder="Enter amount in coin"
        bind:value={amount}
        required
      />
    </div>

    <button class="btn btn-full" on:click={() => (submitted = true)}
      >Convert</button
    >
  </form>
</div>

<!-- <link
  href="https://gist.githubusercontent.com/Ajax30/08899d40e16069cd517b9756dc900acc/raw/04e4f9997245df079fa8500690d1878311115b20/global.css"
  rel="stylesheet"
  crossorigin="anonymous"
/> -->
<style>
  .container {
    max-width: 1200px;
    margin: 0 auto;
  }

  h2 {
    margin-top: 0;
  }

  .form-group > *,
  .btn-full {
    width: 100%;
  }

  .form-control,
  .btn-full {
    border-radius: 3px;
  }

  .submitted input:invalid {
    border: 1px solid #c00;
  }

  .submitted input:focus:invalid {
    outline: 1px solid #c00;
  }

  .error-alert {
    border: 1px solid #c00 !important;
    padding: 6px;
    text-align: center;
    color: #c00;
    border-radius: 3px;
  }
</style>
