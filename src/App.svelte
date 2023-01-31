<script>
  const API =
    'https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&sparkline=false';
  const titles = ['Rank', 'Coin', 'Price', 'Price change'];
  let coins = [];
  let filteredCoins = [];

  const loadCoins = async () => {
    const response = await fetch(API);
    const data = await response.json();
    console.log(data);

    coins = data;
    filteredCoins = data;
  };
  loadCoins();
</script>

<main>
  <header>
    <h1>CryptoMarket</h1>
  </header>

  <div>
    <table class="coins">
      <thead>
        <tr class="coins__titles">
          {#each titles as title}
            <th class="coins__title">{title}</th>
          {/each}
        </tr>
      </thead>

      <tbody class="coins__data">
        {#each coins as coin}
          <tr class="coin">
            <td class="coin__rank">{coin.market_cap_rank}</td>

            <td>
              <picture>
                <img
                  class="coin__logo"
                  src={coin.image}
                  alt={coin.name}
                  height="14"
                />
              </picture>
              <span class="coin__name">{coin.name}</span>
              <span class="coin__symbol">{coin.symbol}</span>
            </td>
          </tr>
        {/each}
      </tbody>
    </table>
  </div>
</main>
