<template>
  <header>
    <router-link to="/">
      <h1>
        <span>Vue</span>
        Movies
      </h1>
    </router-link>
  </header>
  <main>
    <router-view />
  </main>
</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Courier New", Courier, monospace;

  &::selection {
    background: transparentize(#403e3e, 0.5);
  }
}

body {
  background-color: #05215a;
}

a {
  text-decoration: none;
}

header{
  margin-left: 40px;
  margin-right: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px 16px;
  background-color: transparent;


  h1{
    color: white;
    font-size: 20px;
  }

  span{
    color: #4982f4;
  }
}
</style>
