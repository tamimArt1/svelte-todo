<script>
  import { createEventDispatcher } from "svelte";
  export let id, text, completed;

  const dispach = createEventDispatcher();

  function triggerUpdate() {
    dispach("update", { id, text, completed });
  }

  function handleDoubleClick() {
    const yes = confirm("DELETE sure?");
    if (yes) {
      dispach("delete", { id });
    }
  }
</script>

<div class="item" class:completed on:dblclick={handleDoubleClick}>
  <input
    type="text"
    class="text-input"
    bind:value={text}
    readonly={completed}
    on:keyup={({ key, target }) => key === "Enter" && target.blur()}
    on:blur={triggerUpdate}
  />
  <input
    type="checkbox"
    class="completed-checkbox"
    bind:checked={completed}
    on:change={triggerUpdate}
  />
</div>

<style>
  .item {
    display: flex;
    align-items: center;
    padding: 15px;
    background-color: #ffffff;
  }

  input[type="text"] {
    font-family: inherit;
  }

  .item.completed {
    background-color: #dddddd;
  }

  .item.completed .text-input {
    color: #555555;
    text-decoration: line-through;
  }

  .item:focus-within {
    background-color: rgba(255, 255, 255, 0.8);
  }

  .text-input {
    flex-grow: 1;
    border: none;
    outline: none;
    background: none;
    font-size: 1em;
  }

  .completed-checkbox {
    margin-left: 15px;
  }
</style>
