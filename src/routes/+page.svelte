<script lang="ts">
  import { goto } from "$app/navigation";
  import { page } from "$app/stores";
  import type { PageData } from "./$types";
  import type { IndexMonster } from "./+page";
  import Monster from "./Monster.svelte";
  import { generations } from "./generations";

  export let data: PageData;

  $: monsterId = $page.url.searchParams.get("monsterId") || "";
  $: monster = data.monsters.find((monster) => monster.id === monsterId);

  $: monsterId2 = $page.url.searchParams.get("monsterId2") || "";
  $: monster2 = data.monsters.find((monster) => monster.id === monsterId2);

  const updateSearchParams = (key: string, value: string) => {
    const searchParams = new URLSearchParams($page.url.searchParams);
    searchParams.set(key, value);
    goto(`?${searchParams.toString()}`);
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

<div class="monsters">
  {#each data.monsters as monster (monster.id)}
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
</style>
