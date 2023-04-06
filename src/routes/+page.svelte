<script>
  import { quintOut } from "svelte/easing";
  import { crossfade } from "svelte/transition";
  import { flip } from "svelte/animate";
  const [send, receive] = crossfade({
    duration: (d) => Math.sqrt(d * 200),

    fallback(node, params) {
      const style = getComputedStyle(node);
      const transform = style.transform === "none" ? "" : style.transform;

      return {
        duration: 600,
        easing: quintOut,
        css: (t) => `
					transform: ${transform} scale(${t});
					opacity: ${t}
				`,
      };
    },
  });

  import { todoList } from "../stores/todoStore";
  import Card from "../miscellaneous/Card.svelte";
  import Form from "../miscellaneous/Form.svelte";

  let List = new Array();
  todoList.subscribe((value) => (List = value));
</script>

<main>
  <Form />
  <section>
    <div class="Left">
      <h2>To do!</h2>
      {#each List.filter((i) => !i.done) as item (item)}
        <label
          for=""
          animate:flip
          in:receive={{ key: item }}
          out:send={{ key: item }}
        >
          <Card Title={item.title} on:click={() => (item.done = !item.done)} />
        </label>
      {/each}
    </div>

    <div class="Right">
      <h2>Done!</h2>
      {#each List.filter((i) => i.done) as item (item)}
        <label
          for=""
          animate:flip
          in:receive={{ key: item }}
          out:send={{ key: item }}
        >
          <Card Title={item.title} on:click={() => (item.done = !item.done)} />
        </label>
      {/each}
    </div>
  </section>
</main>

<style>
  main {
    width: 80%;
    margin: auto;
    display: grid;
    grid-template-rows: 250px 1fr;
    justify-content: center;
  }
  section {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10em;
  }
</style>
