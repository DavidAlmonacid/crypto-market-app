<script>
  const API =
    'https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&sparkline=false';
  const titles = ['Rank', 'Coin', 'Price', 'Price change'];
  let coins = [];
  let filteredCoins = [];

  const getCoins = async () => {
    try {
      const response = await fetch(API);
      const data = await response.json();
      coins = data;
      filteredCoins = data;
    } catch (error) {
      console.error(error);
    }
  };
  getCoins();
</script>

<main>
  <header>
    <h1>CryptoMarket</h1>
  </header>

  <div>
    <div class="coins">
      {#each titles as title}
        <div>
          <h4 class="coins-title">{title}</h4>
        </div>
      {/each}

      {#each coins as coin}
        <div class="coin-rank">
          <span>{coin.market_cap_rank}</span>
        </div>

        <div class="coin-data">
          <picture>
            <img
              class="coin-logo"
              src={coin.image}
              alt={coin.name}
              height="14"
            />
          </picture>
          <span class="coin-name">{coin.name}</span>
          <span class="coin-symbol">{coin.symbol}</span>
        </div>

        <div class="coin-price">
          <span>$</span>
          <span>{coin.current_price.toLocaleString()}</span>
        </div>

        <div
          class={`coin-change coin-change--${
            coin.price_change_percentage_24h > 0 ? 'up' : 'down'
          }`}
        >
          <span>{coin.price_change_percentage_24h.toFixed(3)}</span>
          <span>%</span>
        </div>
      {/each}
    </div>
  </div>
</main>

<style>
  .coins {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
  }
</style>
