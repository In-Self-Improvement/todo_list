<script>
  import TodoItem from "./TodoItem.svelte";
  export let todoList;
  export let handleComplete;
  export let deleteTodo;
</script>

<div>
  {#each todoList as todo}
    <TodoItem {todo} {handleComplete} {deleteTodo} />
  {/each}
</div>
