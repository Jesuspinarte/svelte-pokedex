<script lang="ts">
  import type { IndexMonster } from "./+page";

  export let monster: IndexMonster;
  export let updateSearchParams: (key: string, value: string) => void;
  export let isInteractive: boolean = false;
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<div class={isInteractive ? "monster is-interactive" : "monster"}>
  <div
    on:click={() =>
      isInteractive ? updateSearchParams("monsterId", monster.id) : {}}
  >
    <div class="monster-content">
      <img src={monster.image} alt={monster.name} />
      {monster.name[0].toUpperCase() +
        monster.name.substring(1).toLocaleLowerCase()}
    </div>
  </div>
  <div class="monster-id">
    {monster.id}
  </div>
  {#if isInteractive}
    <div
      class="monster-btn-2"
      on:click={() => updateSearchParams("monsterId2", monster.id)}
    >
      Add Monster 2
    </div>
  {/if}
</div>

<style>
  .monster-id {
    position: absolute;
    top: 8px;
    left: 8px;
    font-size: 0.8em;
    color: #aaa;
    font-family: Arial, Helvetica, sans-serif;
  }
  .monster {
    width: 130px;
    margin: 10px;
    padding: 10px;
    position: relative;
    background-color: #444;
    border-radius: 4px;
  }
  .is-interactive {
    cursor: pointer;
  }
  .is-interactive:hover {
    background-color: #777;
  }
  .monster-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    color: #ddd;
    font-family: Arial, Helvetica, sans-serif;
  }
  .monster-btn-2 {
    color: #fff;
    text-align: center;
    padding: 4px;
    margin-top: 12px;
    font-family: Arial, Helvetica, sans-serif;
  }
  .monster-btn-2:hover {
    color: #111;
    background-color: #eee;
    opacity: 0.8;
    border-radius: 4px;
  }
</style>
