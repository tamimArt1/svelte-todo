<script>
  import Header from "./components/Header.svelte";
  import List from "./components/List.svelte";
</script>

<h1>SVELTE TODO APP</h1>
<div class="container">
  <Header />
  <List />
</div>

<style>
  h1 {
    text-align: center;
    margin: 1em;
    color: greenyellow;
    font-size: 3rem;
  }
  .container {
    width: 50%;
    background-color: rgba(156, 175, 112, 0.4);
    margin: 0 auto;
  }
</style>
