<script>
  import { onMount } from "svelte";
  import TodoApi from "../todoApi";
  import { items } from "../stores";
  import Item from "./Item.svelte";
  import Input from "./Input.svelte";

  function handleNewItem(e) {
    const newTodo = {
      id: $items.length + 1,
      text: e.detail.value,
      completed: false,
    };
    $items = [...$items, newTodo];
    TodoApi.save(items);
  }

  function handleUpdate(e) {
    const index = $items.findIndex((item) => item.id === e.detail.id);
    $items[index] = e.detail;
    $items.sort((a, b) => {
      if (a.completed && b.completed) return 0;
      if (a.completed) return 1;
      if (b.completed) return -1;
    });
    TodoApi.save($items);
  }

  function handleDelete(e) {
    $items = $items.filter((item) => item.id !== e.detail.id);
    TodoApi.save($items);
  }

  onMount(async () => {
    $items = await TodoApi.getAll();
  });
</script>

<div class="list">
  <Input on:newitem={handleNewItem} />
  {#each $items as item (item.id)}
    <Item {...item} on:update={handleUpdate} on:delete={handleDelete} />
  {:else}
    <p class="no-warning">No item</p>
  {/each}
</div>

<style>
  .list {
    padding: 1em;
    color: white;
    font-size: 20px;
  }
  .no-warning {
    font-size: 3rem;
    font-weight: bold;
    color: yellow;
    text-align: center;
  }
</style>
