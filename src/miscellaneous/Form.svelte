<script>
  import { todoList } from "../stores/todoStore";

  let itemTitle = new String();

  const AddNewItem = () => {
    if (itemTitle.length <= 0) return;
    // @ts-ignore
    todoList.update((value) => [...value, { title: itemTitle, done: false }]);
  };
</script>

<section>
  <div>
    <label for="">Write a Title</label><br />
    <input
      type="text"
      bind:value={itemTitle}
      placeholder="set a title for an item"
    />
  </div>
  <button on:click={AddNewItem}>ADD NEW ONE</button>
</section>

<style>
  section {
    border: 5px solid white;
    padding: 15px;
    font-size: 2rem;
    display: grid;
    justify-content: center;
  }
  section * {
    font-size: 2rem;
  }
  button {
    border: 2px solid white;
    background-color: unset;
    color: white;
    border-radius: 25px;
    cursor: pointer;
    transition: 0.6s;
  }
  button:hover {
    background-color: white;
    color: #242424;
  }
</style>
