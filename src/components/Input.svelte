<!-- JAVASCRIPT -->
<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();
  let value = "";
  function handleKeyUp({ key }) {
    if (key !== "Enter" || value.length === 0) return;
    dispatch("newitem", { value });
    value = "";
  }
</script>

<!-- HTML -->
<div class="new">
  <input
    class="new"
    type="text"
    on:keyup={handleKeyUp}
    bind:value
    placeholder="+ Add Item"
  />
</div>

<!-- CSS -->
<style>
  .new {
    display: flex;
    align-items: center;
    padding: 15px;
    background-color: rgb(189, 187, 187);
  }

  .new:focus-within {
    background-color: rgba(255, 255, 255, 0.8);
  }

  input[type="text"] {
    font-family: inherit;
    flex-grow: 1;
    border: none;
    outline: none;
    font-size: 1em;
  }
</style>
