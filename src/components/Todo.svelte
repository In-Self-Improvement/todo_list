<script>
  import TodoItem from "./TodoItem.svelte";
  export let todoList;
  export let handleComplete;
  export let deleteTodo;
  export let editTodo;
  export let cancelEditTodo;
  export let filteredTodoList;
  export let filterType;
</script>

<div>
  {#if filterType !== "All"}
    {#each filteredTodoList as todo}
      <TodoItem
        {todo}
        {handleComplete}
        {deleteTodo}
        {editTodo}
        {cancelEditTodo}
      />
    {/each}
  {:else}
    {#each todoList as todo}
      <TodoItem
        {todo}
        {handleComplete}
        {deleteTodo}
        {editTodo}
        {cancelEditTodo}
      />
    {/each}
  {/if}
</div>
