<script lang="ts">
  import Header from '$lib/Header/index.svelte';
  import Icon from '$lib/Icon/index.svelte';
  import '../app.css';
</script>

<svelte:head>
  <link rel="preconnect" href="https://fonts.gstatic.com" />
  <link
    rel="preload"
    href="https://fonts.googleapis.com/css2?family=Raleway:wght@100;300;400;900&display=swap"
    as="style"
  />
  <noscript>
    <link
      rel="stylesheet"
      href="https://fonts.googleapis.com/css2?family=Raleway:wght@100;300;400;900&display=swap"
    />
  </noscript>
</svelte:head>

<Header />

<main>
  <slot />
</main>

<footer>
  <p>
    Developed with
    <Icon icon="favorite" className="favorite" />
    by
    <a
      href="https://www.linkedin.com/in/mozart-tomazetti/"
      target="_blank"
      rel="external noopener noreferrer"
    >
      Mozart Pistori Tomazetti
    </a>
  </p>
</footer>

<style lang="scss">
  main {
    flex: 1;
    display: flex;
    flex-direction: column;
    padding: 1rem;
    width: 100%;
    max-width: 1024px;
    margin: var(--column-margin-top) auto 0;
    box-sizing: border-box;
  }

  footer {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 40px 0;
  }
  :global(.favorite) {
    fill: var(--accent-color);
    position: relative;
    top: 0.3rem;
  }
</style>
