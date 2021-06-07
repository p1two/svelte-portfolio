<script lang="ts">
  import { page } from '$app/stores';
  import Icon from '$lib/Icon/index.svelte';
  import Headroom from '$lib/Headroom/index.svelte';
  import logo from './svelte-logo.svg';
</script>

<Headroom offset={48}>
  <header>
    <div class="corner">
      <a href="https://kit.svelte.dev" target="_blank" rel="external noopener noreferrer">
        <img src={logo} alt="SvelteKit" />
      </a>
    </div>

    <nav>
      <svg viewBox="0 0 2 3" aria-hidden="true">
        <path d="M0,0 L1,2 C1.5,3 1.5,3 2,3 L2,0 Z" />
      </svg>
      <ul>
        <li class:active={$page.path === '/'}><a sveltekit:prefetch href="/">Home</a></li>
        <li class:active={$page.path === '/projects'}>
          <a sveltekit:prefetch href="/projects">Projects</a>
        </li>
        <li class:active={$page.path === '/todos'}>
          <a sveltekit:prefetch href="/todos">Todos</a>
        </li>
      </ul>
      <svg viewBox="0 0 2 3" aria-hidden="true">
        <path d="M0,0 L0,3 C0.5,3 0.5,3 1,2 L2,0 Z" />
      </svg>
    </nav>

    <div class="corner">
      <a
        href="https://github.com/pitwo42"
        class="github"
        aria-label="Github"
        target="_blank"
        rel="external noopener noreferrer"
      >
        <Icon icon="github" width="32" height="32" />
      </a>
    </div>
  </header>
</Headroom>

<style lang="scss">
  :global(.headroom.unpin),
  :global(.headroom.scroll) {
    z-index: 1;
    background: linear-gradient(116.82deg, var(--primary-color) 0%, #2b3b48 100%);
    box-shadow: 0 0 0.5em rgba(0, 0, 0, 0.5);
  }

  header {
    display: flex;
    justify-content: space-between;
  }

  .corner {
    width: 3em;
    height: 3em;
    a {
      display: flex;
      align-items: center;
      justify-content: center;
      width: 100%;
      height: 100%;
      &.github {
        fill: var(--pure-white);
        &:hover {
          fill: var(--accent-color);
        }
      }
    }
    img {
      width: 2em;
      height: 2em;
      object-fit: contain;
    }
  }

  nav {
    display: flex;
    justify-content: center;
    --background: rgba(255, 255, 255, 0.7);
    a {
      display: flex;
      height: 100%;
      align-items: center;
      padding: 0 1em;
      color: var(--heading-color);
      font-weight: 700;
      font-size: 0.8rem;
      text-transform: uppercase;
      letter-spacing: 10%;
      text-decoration: none;
      transition: color 0.2s linear;
      &:hover {
        color: var(--accent-color);
      }
    }
  }

  svg {
    width: 2em;
    height: 3em;
    display: block;
  }

  path {
    fill: var(--background);
  }

  ul {
    position: relative;
    padding: 0;
    margin: 0;
    height: 3em;
    display: flex;
    justify-content: center;
    align-items: center;
    list-style: none;
    background: var(--background);
    background-size: contain;
  }

  li {
    position: relative;
    height: 100%;
  }

  li.active::before {
    --size: 6px;
    content: '';
    width: 0;
    height: 0;
    position: absolute;
    top: 0;
    left: calc(50% - var(--size));
    border: var(--size) solid transparent;
    border-top: var(--size) solid var(--accent-color);
  }
</style>
