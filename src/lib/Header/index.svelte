<script lang="ts">
  import { page } from '$app/stores';
  import logo from './svelte-logo.svg';
  import Icon from 'fa-svelte';
  import { faGithub } from '@fortawesome/free-brands-svg-icons/faGithub';
</script>

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
      <li class:active={$page.path === '/projects'}><a sveltekit:prefetch href="/projects">Projects</a></li>
      <li class:active={$page.path === '/todos'}><a sveltekit:prefetch href="/todos">Todos</a></li>
    </ul>
    <svg viewBox="0 0 2 3" aria-hidden="true">
      <path d="M0,0 L0,3 C0.5,3 0.5,3 1,2 L2,0 Z" />
    </svg>
  </nav>

  <div class="corner">
    <a
      href="https://github.com/pitwo42"
      aria-label="My Github"
      target="_blank"
      rel="external noopener noreferrer"
    >
      <Icon icon={faGithub} definition="Github" />
    </a>
  </div>
</header>

<style lang="scss">
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
    }
    img,
    :global(svg) {
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