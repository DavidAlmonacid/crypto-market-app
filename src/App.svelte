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
      coins = [...data];
      filteredCoins = [...data];
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
    <div class="table-wrapper">
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

              <td class="coin__data">
                <picture class="coin__logo-wrapper">
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

              <td class="coin__price">
                <span>$</span><span>{coin.current_price.toLocaleString()}</span>
              </td>

              <td
                class={`coin__change coin__change--${
                  coin.price_change_percentage_24h > 0 ? 'up' : 'down'
                }`}
              >
                <span>{coin.price_change_percentage_24h.toLocaleString()}</span
                ><span>%</span>
              </td>
            </tr>
          {/each}
        </tbody>
      </table>
    </div>
  </div>
</main>

<style>
  main {
    padding: 0 16px;
  }

  main > div {
    margin-top: 32px;
    max-height: 84vh;
    overflow: auto;
  }

  .table-wrapper {
    margin: 0 auto;
    padding: 0 12px 12px 0;
    width: fit-content;
  }

  .coins {
    border-collapse: collapse;
    border-radius: 12px;
    background-color: #084c61;
    text-align: center;
  }

  .coins__titles :nth-child(n + 3) {
    width: 120px;
  }

  .coins__data > tr:nth-child(odd) {
    background-color: #105961;
  }

  .coins__title {
    font-size: 14.5px;
    font-weight: 500;
  }

  .coins th,
  .coins td {
    padding: 10px;
  }

  .coin__data {
    text-align: start;
    white-space: nowrap;
  }

  .coin__logo-wrapper {
    margin-right: 8px;
    vertical-align: middle;
  }

  .coin__symbol {
    margin-left: 8px;
    border-radius: 4px;
    padding: 0 4px;
    background-color: #6e4c6e;
    font-size: 12px;
    font-weight: 500;
    text-transform: uppercase;
    opacity: 0.84;
  }

  .coin__change--up {
    color: #b5da95;
  }

  .coin__change--down {
    color: #f28e8e;
  }
</style>
