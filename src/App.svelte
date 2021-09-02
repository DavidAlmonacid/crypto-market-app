<script>
const titles = ['Rank', 'Coin', 'Price', 'Price change']
let coins = []
let filteredCoins = []

const loadCoins = async () => {
  const res = await fetch(
    'https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1'
  )

  const data = await res.json()
  console.log(data)
  coins = data
  filteredCoins = data
}
loadCoins()

const searchCoin = (value) => {
  filteredCoins = coins.filter(
    (coin) =>
      coin.name.toLowerCase().includes(value.toLowerCase()) ||
      coin.symbol.toLowerCase().includes(value.toLowerCase())
  )
}
</script>

<div class="headerContainer">
  <header class="header">
    <h1 class="header__title">CRYPTO</h1>
    <div class="header__inputContainer">
      <svg
        class="header__searchIcon"
        width="14"
        height="14"
        viewBox="0 0 14 14"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M8.34486 0.896875C7.4259 0.89601 6.52733 1.17624 5.76283 1.70211C4.99833 2.22799 4.40225 2.97588 4.05 3.85117C3.69774 4.72647 3.60514 5.68984 3.78391 6.61942C3.96268 7.549 4.40478 8.40301 5.05429 9.07343C5.7038 9.74385 6.53153 10.2005 7.43277 10.3858C8.33402 10.571 9.26828 10.4763 10.1174 10.1139C10.9665 9.75142 11.6922 9.13739 12.2029 8.34948C12.7135 7.56157 12.9861 6.63518 12.9861 5.6875C12.9805 4.41947 12.4899 3.20496 11.6208 2.30791C10.7517 1.41086 9.57446 0.903779 8.34486 0.896875V0.896875ZM8.34486 0C9.43566 0 10.502 0.333566 11.4089 0.958517C12.3159 1.58347 13.0228 2.47173 13.4402 3.51099C13.8576 4.55024 13.9668 5.69381 13.754 6.79708C13.5412 7.90034 13.016 8.91376 12.2447 9.70917C11.4734 10.5046 10.4906 11.0463 9.42081 11.2657C8.35098 11.4852 7.24207 11.3725 6.2343 10.9421C5.22654 10.5116 4.36519 9.78261 3.75918 8.84731C3.15317 7.912 2.82971 6.81238 2.82971 5.6875C2.82971 4.17908 3.41077 2.73244 4.44506 1.66583C5.47935 0.599217 6.88215 0 8.34486 0Z"
          fill="white"
          fill-opacity="0.5"
        />
        <path
          d="M0.424229 13.2519L3.5509 10.0056L4.15332 10.6225L1.02665 13.8687C0.987376 13.9095 0.940692 13.942 0.889267 13.9641C0.837843 13.9863 0.782685 13.9979 0.726941 13.9981C0.671198 13.9983 0.615963 13.9871 0.564387 13.9653C0.512812 13.9435 0.465907 13.9114 0.426351 13.8709C0.386795 13.8304 0.355363 13.7823 0.333849 13.7293C0.312335 13.6762 0.301159 13.6193 0.300962 13.5619C0.300765 13.5044 0.31155 13.4474 0.3327 13.3942C0.35385 13.341 0.384952 13.2927 0.424229 13.2519Z"
          fill="white"
          fill-opacity="0.5"
        />
      </svg>

      <input
        type="text"
        class="header__input"
        placeholder="Search coin"
        on:keyup={({ target: { value } }) => searchCoin(value)}
      />
    </div>
  </header>
</div>

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
      {#each filteredCoins as coin}
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
/* start header styles */

.headerContainer {
  max-width: 420px;
  margin: 0 auto;
  padding: 0 5px 15px;
}

.header {
  display: flex;
  align-items: center;
  justify-content: space-evenly;
  background-color: #1e212b;
  border-radius: 12px;
}

.header__title {
  font-size: 22px;
  text-align: center;
}

.header__inputContainer {
  display: flex;
  align-items: center;
  background-color: #2a2e3c;
  border-radius: 7px;
  margin: 12px;
}

.header__searchIcon {
  box-sizing: content-box;
  padding: 0 3px 0 9px;
}

.header__input {
  box-sizing: content-box;
  width: 200px;
  height: 23px;
  font: inherit;
  color: rgba(255, 255, 255, 0.8);
  padding: 1px 5px;
  background-color: #2a2e3c;
  border: 0;
  border-radius: 7px;
  outline: 0;
}

.header__input::-webkit-input-placeholder {
  color: rgba(255, 255, 255, 0.5);
}

/* start table styles */
.tableCoins {
  width: 100%;
  border-collapse: collapse;
  margin: 0 auto;
}

@media screen and (min-width: 425px) {
  .tableCoins {
    width: auto;
    min-width: 408.22px;
  }
}

.tableCoins__headRow > [class*='tableCoins'],
.tableCoins__bodyRow > [class*='tableCoins'] {
  padding: 3px;
}

.tableCoins__headRow :nth-child(2) {
  text-align: left;
  padding: 3px 17px;
}

.tableCoins__body > [class*='bodyRow']:nth-child(2n + 1) {
  background-color: #2a2e3c;
}

.tableCoins__body > [class*='bodyRow']:nth-child(2n + 1):hover {
  background-color: #363b4d;
}

.tableCoins__body > [class*='bodyRow']:nth-child(2n + 2) {
  background-color: #322a3c;
}

.tableCoins__body > [class*='bodyRow']:nth-child(2n + 2):hover {
  background-color: #40364d;
}

.tableCoins__rank {
  opacity: 0.5;
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
  opacity: 0.5;
  text-transform: uppercase;
}

[class*='price'] {
  text-align: right;
}

.tableCoins__priceChange--textSuccess {
  color: #34b21a;
}

.tableCoins__priceChange--textDanger {
  color: #f66;
}
</style>
