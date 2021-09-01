<script>
  let coins = []

  const loadCoins = async () => {
    const res = await fetch(
      'https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1'
    )

    const data = await res.json()
    console.log(data)
    coins = data
  }

  loadCoins()

  const titles = ['Rank', 'Coin', 'Price', 'Price change']
</script>

<header class="header">
  <h1>Coin Market</h1>
</header>

<main class="mainContent">
  <table class="tableCoins">
    <thead class="tableCoins__head">
      <tr class="tableCoins__headRow">
        {#each titles as title}
          <th class="tableCoins__title">{title}</th>
        {/each}
      </tr>
    </thead>

    <tbody class="tableCoins__body">
      {#each coins as coin}
        <tr class="tableCoins__bodyRow">
          <td class="tableCoins__rank">{coin.market_cap_rank}</td>
          <td class="tableCoins__coin">
            <img
              class="tableCoins__coinLogo"
              src={coin.image}
              alt={coin.name}
              height="15.5"
            />
            <span class="tableCoins__coinName">{coin.name}</span>
            <span class="tableCoins__coinSymbol">{coin.symbol}</span>
          </td>
          <td class="tableCoins__price">${coin.current_price.toLocaleString()}</td>
          <td
            class={coin.price_change_percentage_24h > 0
              ? 'tableCoins__priceChange tableCoins__priceChange--textSuccess'
              : 'tableCoins__priceChange tableCoins__priceChange--textDanger'}
          >
            {coin.price_change_percentage_24h.toFixed(3)}%
          </td>
        </tr>
      {/each}
    </tbody>
  </table>
</main>

<style>
  .header {
    text-align: center;
    padding: 10px 0;
  }

  .tableCoins {
    border-collapse: collapse;
    background-color: #bcbcaa;
    margin: 0 auto;
  }

  .tableCoins__head {
    background-color: #b7b7a4;
  }

  .tableCoins__headRow > [class^='tableCoins'],
  .tableCoins__bodyRow > [class^='tableCoins'] {
    padding: 3px;
  }

  .tableCoins__body > *:hover {
    background-color: #b7b7a4;
  }

  .tableCoins__rank {
    opacity: 0.8;
    text-align: center;
  }

  .tableCoins__coin {
    display: flex;
    align-items: center;
  }

  .tableCoins__coin :nth-child(1n + 2) {
    margin-left: 7px;
  }

  .tableCoins__coinSymbol {
    opacity: 0.8;
    text-transform: uppercase;
  }

  [class*='price'] {
    text-align: right;
  }

  .tableCoins__priceChange--textSuccess {
    color: #095809;
  }

  .tableCoins__priceChange--textDanger {
    color: #832a2a;
  }
</style>
