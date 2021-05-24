<script lang="ts">
  import Header from '$lib/Header/index.svelte';
  import '../app.css';
</script>

<svelte:head>
  <link rel="preconnect" href="https://fonts.gstatic.com" />
  <link
    rel="preload"
    href="https://fonts.googleapis.com/css2?family=Raleway:wght@100;300;400;900&display=swap"
    as="style"
  />
  <noscript
    ><link
      rel="stylesheet"
      href="https://fonts.googleapis.com/css2?family=Raleway:wght@100;300;400;900&display=swap"
    /></noscript
  >
</svelte:head>

<Header />

<main>
  <slot />
</main>

<footer>
  <p>Developed by <a href="https://mozartomazetti.netlify.app">Mozart Pistori Tomazetti</a></p>
</footer>

<style lang="scss">
  main {
    flex: 1;
    display: flex;
    flex-direction: column;
    padding: 1rem;
    width: 100%;
    max-width: 1024px;
    margin: 0 auto;
    box-sizing: border-box;
  }

  footer {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 40px 0;
  }
</style>
