<script>
  export let filterAll
  export let filterActive
  export let filterCompleted
  export let filterType
</script>

<div>
  <button class={filterType === 'All' ? 'selected' : ''} on:click={filterAll}>All</button>
  <button class={filterType === 'Active' ? 'selected' : ''} on:click={filterActive}>Active</button>
  <button class={filterType === 'Completed' ? 'selected' : ''} on:click={filterCompleted}>Completed</button>
</div>

<style>
 button:active {
  background-color: #ffffff;
  color: black;
 }
 .selected{
  background-color: red;
 }
</style>
