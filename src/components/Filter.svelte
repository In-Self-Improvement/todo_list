<script>
  export let filterAll
  export let filterActive
  export let filterCompleted
  export let filterNum
</script>

<div>
  <button class={filterNum === 'All' ? 'selected' : ''} on:click={filterAll}>All</button>
  <button class={filterNum === 'Active' ? 'selected' : ''} on:click={filterActive}>Active</button>
  <button class={filterNum === 'Completed' ? 'selected' : ''} on:click={filterCompleted}>Completed</button>
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
