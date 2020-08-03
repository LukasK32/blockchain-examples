<template>
  <div class="APP">
    <main>
      <Nuxt />
    </main>
    <footer>
      <div>
        <!-- Copyright 2020 -->
      </div>
      <div>
        Examples:
        <nuxt-link to="/blockchain">
          Blockchain
        </nuxt-link>
        <nuxt-link to="/">
          Mining
        </nuxt-link>
      </div>
    </footer>
  </div>
</template>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Nunito&family=Roboto+Mono&display=swap');

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

  & > footer {
    flex: 0;
  }
}

.APP > main {
  width: 100%;
  max-width: 900px;

  padding: 30px 20px;
}

.APP > footer {
  background-color: #414141;
  padding: 10px 30px;
  width: 100%;

  display: flex;
  justify-content: space-between;
  align-content: flex-start;
  align-items: flex-start;

  flex-direction: column;

  @media all and (min-width: 600px) {
    flex-direction: row;
  }

  & > div {
    padding: 5px 0;
  }

  a {
    color: inherit;
    text-decoration: none;

    &:hover {
      color: #fff;
      text-decoration: underline;
    }
  }
}

p {
  text-align: justify;
}
</style>
