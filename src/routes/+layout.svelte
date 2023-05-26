<script lang="ts">
  import { page } from "$app/stores";
</script>

<div class="navbar">
  <a href="/" class:active={$page.url.pathname == "/"}>Home</a>
  <a href="/my-monsters" class:active={$page.url.pathname == "/my-monsters"}
    >My Monsters</a
  >
</div>

<div class="container">
  <slot />
</div>

<style>
  .navbar {
    font-family: Arial, Helvetica, sans-serif;
    display: flex;
    justify-content: center;
    background-color: #333;
    color: #fff;
    padding: 15px;
    margin-bottom: 30px;
  }

  .navbar a {
    color: #fff;
    text-decoration: none;
    padding: 4px 12px;
    border-right: 1px solid #777;
  }

  .navbar a:last-child {
    border-right: none;
  }

  .navbar a.active {
    color: #999;
  }

  .navbar a:hover {
    color: #ccc;
  }

  :global(body) {
    margin: 0;
  }

  .container {
    max-width: 90%;
    margin: 0 auto;
    width: 1200px;
  }
</style>
