<script>
  export let todo;
  export let handleComplete;

  $: completed = todo.completed ? "line-through" : "none";
</script>

<div>
  <input
    type="checkbox"
    checked={todo.completed}
    on:change={() => handleComplete(todo.id)}
  />
  <p style="text-decoration: {completed}">{todo.text}</p>
</div>

<style>
  div {
    display: flex;
  }
</style>
