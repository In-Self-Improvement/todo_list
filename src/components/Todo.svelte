<script>
  import TodoItem from "./TodoItem.svelte";
  export let todoList;
  export let handleComplete;
  export let deleteTodo;
  export let editTodo;
</script>

<div>
  {#each todoList as todo}
    <TodoItem {todo} {handleComplete} {deleteTodo} {editTodo} />
  {/each}
</div>
