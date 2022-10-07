<script>
  export let todo;
  export let handleComplete;
  export let deleteTodo;
  $: completed = todo.completed ? "line-through" : "none";
</script>

<div>
  <input
    type="checkbox"
    checked={todo.completed}
    on:change={() => handleComplete(todo.id)}
  />
  <p style="text-decoration: {completed}">{todo.text}</p>
  <button on:click={() => deleteTodo(todo.id)}>X</button>
</div>

<style>
  div {
    display: flex;
  }
</style>
