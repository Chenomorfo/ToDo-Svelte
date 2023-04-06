<script>
  export let Title = "No title";
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<div on:click>
  <h1>{Title}</h1>
</div>

<style>
  div {
    max-width: 200px;
    border: 3px solid white;
    margin: 5px;
    padding: 5px 10px;
    text-align: center;
    user-select: none;
    cursor: pointer;
  }
</style>
