<script lang="ts">
  import { onMount } from 'svelte';
  import Icon from 'fa-svelte';
  import { faVuejs } from '@fortawesome/free-brands-svg-icons';

  let promise = Promise.resolve([]);
  let data = [];
  let projects = [];
  let skills: Array<string> = [];
  let page = 1;
  const perPage = 6;

  $: {
    projects = projects.concat(data);
    projects.forEach((project: { language: string }) => {
      if (project.language !== null && !skills.includes(project.language)) {
        skills = [...skills, project.language];
      }
    });
  }
  async function fetchData() {
    let response = await fetch(
      `https://api.github.com/users/pitwo42/repos?per_page=${perPage}&page=${page}`
    );
    data = await response.json();
    if (response.ok) {
      return data;
		} else {
			throw new Error(data.message);
		}
  }
  function loadMore(): void {
    page++;
    fetchData();
  }
  function trimTitle(text: string): string {
    let title = text.replaceAll("-", " ").replaceAll("_", " ");
    if(title.length > 16) {
      return title.slice(0, 15) + ' ...';
    }
    return title;
  }
  function trimText(text: string): string {
    if(text.length > 121) {
      return text.slice(0, 120) + ' ...';
    }
    return text;
  }
  onMount(() => {
    promise = fetchData();
  });
</script>

<svelte:head>
  <title>Mozart's Projects</title>
  <meta name="description" content="Mozart's projects and skills list" />
</svelte:head>

{#await promise}
  <div class="loading">😴 Loading ...</div>
{:then data}
  <section id="portfolio" v-else>
    <h2>Projets</h2>
    <div class="cards d_flex">
      {#each projects as project}
        <div class="card__custom">
          <div class="card__custom__text">
            <div>
              <h3>{trimTitle(project.name)}</h3>
              <p>{trimText(project.description)}</p>
            </div>
            <div class="meta__data d_flex">
              <div class="date">
                <h4>Updated at</h4>
                <div>{new Date(project.updated_at).toDateString()}</div>
              </div>
              <img class="avatar" src={project.owner.avatar_url} alt="Repository owner avatar" />
            </div>
          </div>
          <div class="card__custom__img" />
          <div class="card_custom__button">
            <a href={project.html_url} target="_blank" rel="external noopener noreferrer"> Code </a>
          </div>
        </div>
      {/each}
    </div>
    {#if projects.length == page * perPage}
      <div style="text-align: center; width:100%">
        <button class="btn_load_more" on:click={loadMore}>Load More</button>
      </div>
    {/if}
    <div id="skills_section">
      <h2>Development Skills</h2>
      <ul class="skills">
        {#each skills as skill}
          <li>{skill}</li>
        {/each}
      </ul>
    </div>
  </section>
{:catch error}
  <div class="error">
    <p>{error.message} 😥</p>
  </div>
{/await}

<style lang="scss">
  .d_flex {
    display: flex;
    flex-wrap: wrap;
  }
  /* Components */
  .cards {
    justify-content: space-between;
  }
  .card__custom {
    position: relative;
    display: flex;
    max-width: 400px;
    height: 300px;
    min-height: 300px;
    padding: 0.5rem;
    margin-bottom: 3rem;
    flex-grow: 1;
    flex-basis: calc(100% / 2 - 1rem);
    align-items: center;
    justify-content: space-between;
    > .card__custom__text {
      max-width: calc((100% / 3) * 2);
      text-align: right;
      height: 80%;
      display: flex;
      flex-direction: column;
      justify-content: space-around;
      overflow: hidden;
    }
  }
  .card__custom__img {
    position: absolute;
    width: 70%;
    height: 100%;
    background-image: url(/img/cards_bg_img.svg);
    background-position: center;
    background-repeat: no-repeat;
    background-size: contain;
    display: inline-block;
    z-index: -1;
    left: 60%;
    transform: translateX(-50%);
    border-radius: 85px 0 100px 25px;
  }
  .card_custom__button a,
  .btn_load_more {
    background: #f1edee;
    border: 5px solid #3d5467;
    box-sizing: border-box;
    border-radius: 54px;
    padding: 0.5rem 1rem;
    font-weight: 900;
    color: #3d5467;
    &:hover {
      cursor: pointer;
      background: #324555;
      color: white;
      border-color: #db5461;
      transition: 1s;
    }
  }
  .card__custom__text h3 {
    text-transform: uppercase;
    font-size: 1.5rem;
  }
  /* END Componenet */
  /* Header */
  #site_header {
    text-align: center;
    padding: 2rem 1rem;
    justify-content: space-between;
    align-items: center;
    > h1 {
      text-transform: uppercase;
    }
  }
  /* Portfolio Page Section */
  #portfolio {
    margin-top: 4rem;
    h2 {
      margin-left: 180px;
      font-size: 44px;
      color: #f1edee;
      line-height: 2rem;
      &:first-child {
        margin-bottom: 4rem;
      }
    }
    .projects {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: space-around;
    }
  }
  /* Skills */
  #skills_section {
    margin-top: 4rem;
    min-height: 300px;
    background-image: url(/img/skills_bg.svg);
    background-repeat: no-repeat;
    background-size: contain;
    background-position: top left;
    ul {
      list-style: none;
      margin: 20px 120px;
      display: flex;
      flex-wrap: wrap;
      li {
        padding: 1rem;
        margin: 0.5rem;
        background-color: #db5461;
        border: 5px solid #3d5467;
        border-radius: 35px;
      }
    }
  }
  .avatar {
    width: 30px;
    height: 30px;
    border-radius: 50%;
    margin: 0 1rem;
  }
  .card__back {
    display: none;
  }
  .rotate__card {
    transform: rotate3d(360, 0, 0, 180deg);
  }
  /* Media Query  */
  @media screen and (max-width: 768px) {
    .cards {
      justify-content: space-evenly
    }
    .card__custom {
      flex-basis: 100%;
    }
    #portfolio h2 {
      margin: 0 0 0 40px;
    }
    #skills_section h2 {
      font-size: 2.5rem;
      color: #db5461;
    }
  }
</style>
