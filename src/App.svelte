<script>
  import { onMount } from 'svelte';
  import Header from './lib/Header.svelte';
  import TableCoins from './lib/TableCoins.svelte';

  const API =
    'https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&sparkline=false';
  const titles = ['Rank', 'Coin', 'Price', 'Price change'];
  let coins = [];
  let filteredCoins = [];

  const getCoins = async () => {
    try {
      const response = await fetch(API);
      const data = await response.json();
      coins = [...data];
      filteredCoins = [...data];
    } catch (error) {
      console.error(error);
    }
  };

  const searchCoins = (event) => {
    const search = event.target.value.toLowerCase();

    filteredCoins = coins.filter((coin) => {
      return (
        coin.name.toLowerCase().includes(search) ||
        coin.symbol.toLowerCase().includes(search)
      );
    });
  };

  onMount(() => {
    getCoins();
  });
</script>

<main>
  <Header {searchCoins} />
  <TableCoins {titles} {filteredCoins} />
</main>

<style>
  main {
    padding: 0 16px;
  }
</style>
