<script lang="ts">
  import { goto } from "$app/navigation";
  import { page } from "$app/stores";
  import type { PageData } from "./$types";
  import type { IndexMonster } from "./+page";
  import Monster from "./Monster.svelte";
  import { generations } from "./generations";

  export let data: PageData;

  let form = {
    searchString: "",
  };

  let searchString = "";

  // $: searchString = form.searchString;

  $: selectedMonsters = data.monsters.filter((monster) =>
    monster.name.toLowerCase().includes(searchString.toLocaleLowerCase())
  );

  $: monsterId = $page.url.searchParams.get("monsterId") || "";
  $: monster = data.monsters.find((monster) => monster.id === monsterId);

  $: monsterId2 = $page.url.searchParams.get("monsterId2") || "";
  $: monster2 = data.monsters.find((monster) => monster.id === monsterId2);

  const updateSearchParams = (key: string, value: string) => {
    const searchParams = new URLSearchParams($page.url.searchParams);
    searchParams.set(key, value);
    goto(`?${searchParams.toString()}`);
  };


  const submitSearch = (e: Event) => {
    e.preventDefault();
    searchString = form.searchString;
  };
</script>

{#if monster}
  <Monster {monster} {updateSearchParams} />
{/if}

{#if monster2}
  <Monster monster={monster2} {updateSearchParams} />
{/if}

<div class="generations">
  {#each generations as generation (generation.id)}
    <div class="generation">
      {generation.main_region}
    </div>
  {/each}
</div>

<form on:submit={submitSearch} class="search-form">
  <input
    type="text"
    bind:value={form.searchString}
    placeholder="Pokémon Name"
  />
  <input class="submit-btn" type="submit" value="Search" />
</form>

<div class="monsters">
  {#each selectedMonsters as monster (monster.id)}
    <Monster {monster} isInteractive {updateSearchParams} />
  {/each}
</div>

<style>
  .generations {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
  }
  .generation {
    margin: 5px;
    padding: 5px 10px;
    border: 1px solid black;
    background-color: #bbb;
    color: #222;
  }
  .generation:hover {
    background-color: #eee;
  }
  .monsters {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
  }

  .search-form {
    display: flex;
    justify-content: center;
    margin: 20px 0;
  }
  .search-form input[type="text"] {
    padding: 5px 10px;
    border: 1px solid #333;
    border-radius: 5px;
    width: 60%;
    background-color: rgba(255, 255, 255, 0.2);
    color: #fff;
  }
  .search-form input[type="text"]::placeholder {
    color: #888;
  }
  .search-form input[type="text"]:focus {
    outline: none;
    border: 1px solid #aaa;
  }
  .search-form input[type="submit"] {
    padding: 5px 10px;
    border: 1px solid #333;
    border-radius: 5px;
    margin-left: 10px;
    background-color: #666;
    color: #fff;
    cursor: pointer;
  }
  .search-form input[type="submit"]:hover {
    background-color: #444;
  }
</style>
