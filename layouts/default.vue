<template>
  <div class="APP">
    <header>
      <div>
        Blockchain examples
      </div>
      <nav>
        <nuxt-link to="/blockchain">
          Blockchain
        </nuxt-link>
        <nuxt-link to="/">
          Mining
        </nuxt-link>
      </nav>
    </header>
    <main>
      <Nuxt />
    </main>
  </div>
</template>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Nunito&family=Roboto+Mono&display=swap');

$headerBreakpoint: 650px;

html {
  font-family: 'Nunito', sans-serif;

  background-color: #313131;
  color: #eee;

  font-size: 20px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
}

.APP {
  display: flex;
  flex-direction: column;
  flex-wrap: nowrap;
  justify-content: space-between;
  align-content: flex-start;
  align-items: center;

  min-height: 100vh;

  & > main {
    flex: 1;
  }

  & > header {
    flex: 0;
  }
}

.APP > main {
  width: 100%;
  max-width: 850px;

  padding: 30px 20px;
}

.APP > header {
  background-color: #414141;
  width: 100%;

  display: flex;
  justify-content: space-between;
  align-content: flex-start;
  align-items: flex-start;

  flex-direction: column;

  @media all and (min-width: $headerBreakpoint) {
    flex-direction: row;
  }

  & > div {
    padding: 15px 30px;
    display: none;

    @media all and (min-width: $headerBreakpoint) {
      display: block;
    }
  }

  & > nav {
    display: flex;
    flex-direction: row;
  }

  a {
    display: inline-block;
    color: inherit;
    text-decoration: none;

    padding: 15px 30px;
    margin: 0;

    &:hover {
      background-color: rgba(0,0,0,0.1);
    }
  }
}

p {
  text-align: justify;
}
</style>
