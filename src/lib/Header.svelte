<script>
  import { onMount } from 'svelte';

  export let searchCoins;

  let ref = null;

  onMount(() => {
    ref.focus();
  });
</script>

<header class="header">
  <div class="header__wrapper">
    <h1 class="header__title">CRYPTO</h1>

    <div class="header__search-wrapper">
      <label for="search">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          width="16"
          class="header__search-icon"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z"
          />
        </svg>
      </label>

      <input
        type="search"
        placeholder="Search coin"
        class="header__search"
        id="search"
        on:input={searchCoins}
        bind:this={ref}
      />
    </div>
  </div>
</header>

<style>
  .header {
    margin: 0 auto;
    padding: 32px 0;
    max-width: 538px;
  }

  .header__wrapper {
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-radius: 12px;
    padding: 12px 8px;
    background-color: #052c39;
  }

  .header__title {
    font-size: 20px;
  }

  .header__search-wrapper {
    display: flex;
    align-items: center;
    gap: 4px;
    border-radius: 10px;
    padding: 4px 8px;
    height: 30px;
    background-color: #084c61;
  }

  .header__search-icon {
    vertical-align: middle;
    transform: rotateY(200deg);
  }

  .header__search {
    align-self: stretch;
    outline: 0;
    border: 0;
    width: 192px;
    background: none;
  }
</style>
