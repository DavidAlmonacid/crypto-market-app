<header class="header">
  <div class="header__wrapper">
    <h1 class="header__title">CRYPTO</h1>

    <div class="header__search-wrapper">
      <label for="search">Search</label>
      <input
        type="search"
        placeholder="Search coin"
        class="header__search"
        id="search"
      />
    </div>
  </div>
</header>

<style>
  .header {
    margin: 0 auto;
    padding: 32px 0;
    max-width: 520px;
  }

  .header__wrapper {
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-radius: 12px;
    padding: 12px 8px;

    /* change */
    background: rebeccapurple;
  }

  .header__title {
    font-size: 20px;
  }

  .header__search-wrapper {
    display: flex;
    align-items: center;
  }
</style>
