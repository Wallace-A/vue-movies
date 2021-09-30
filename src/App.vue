<template>
  <header>
    <router-link to="/">
      <h1><span>Vue</span>Movies</h1>
    </router-link>
  </header>
  <main>
    <router-view/>
  </main>
  <footer>
    
  </footer>
</template>

<style lang="scss">
  *{
    margin: 4;
    padding: 0;
    box-sizing:border-box;
    font-family: "Fira Sans", sans-serif; 
    &::selection {
      background: transparent(#42BB83, 0.5);
    }
  }
  

  body {
    background-color: #35495E;
  }
</style>
