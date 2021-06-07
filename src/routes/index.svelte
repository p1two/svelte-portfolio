<script context="module" lang="ts">
  export const prerender = true;
</script>

<svelte:head>
  <title>Mozart's Portfolio</title>
  <meta name="description" content="Mozart's information" />
</svelte:head>

<section>
  <div class="about__me">
    <picture>
      <source srcset="/img/avatar.webp" type="image/webp" />
      <img src="/img/avatar.jpeg" alt="Mystery Person" width="200" height="200" />
    </picture>
    <h1>Mozart Pistori Tomazetti</h1>
    <h2>Go and Svelte Enthusiast</h2>
    <div class="skills_projects_link">
      <a href="/projects">Projects/Skills</a>
    </div>
  </div>
</section>

<style lang="scss">
  section {
    width: 100%;
    height: 88vh;
    min-height: 576px;
    display: flex;
    justify-content: center;
    align-items: center;
    > .about__me {
      text-align: center;
      width: 80%;
      line-height: 1.5rem;
      > h1 {
        margin: 20px 0 0;
        font-size: 36px;
        font-weight: 900;
        color: var(--accent-color);
      }
      > h2 {
        font-size: 28px;
        font-weight: 500;
      }
      > h1,
      > h2 {
        font-style: normal;
        line-height: 42px;
        letter-spacing: 0.115em;
      }
      p {
        font-weight: 100;
        font-size: 22px;
        padding: 2rem;
      }
    }
  }
  .skills_projects_link {
    position: relative;
    > a {
      text-transform: uppercase;
      font-weight: 900;
      font-size: 18px;
      line-height: 21px;
      &:hover {
        transition: all 0.5s ease-in-out;
        &::after {
          position: absolute;
          left: 50%;
          transform: translateX(-50%);
          display: flex;
          margin: auto;
          text-align: center;
          content: '';
          width: 30px;
          height: 2px;
          background-color: #db5461;
          transition: background-color 0.5s ease-in-out;
        }
      }
    }
  }
</style>
