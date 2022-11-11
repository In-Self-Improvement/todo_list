<script>
  export let todo;
  export let handleComplete;
  export let deleteTodo;
  export let cancelEditTodo;
  export let editTodo;

  $: completed = todo.completed ? "line-through" : "none";
  let editMode = false;
  let temp;
  const openEditMode = () => {
    editMode = true;
    temp = todo.text;
  };
  const closeEitMode = () => {
    editMode = false;
  };
</script>

<div>
  {#if editMode}
    <input type="text" bind:value={todo.text} />
    <button
      on:click={() => {
        closeEitMode();
        cancelEditTodo(todo.id, temp);
      }}>cancel</button
    >
    <button
      on:click={() => {
        editTodo(todo.id, todo.text);
        closeEitMode();
      }}>enter</button
    >
  {:else}
    <input
      type="checkbox"
      checked={todo.completed}
      on:change={() => handleComplete(todo.id)}
    />
    <p style="text-decoration: {completed}">{todo.text}</p>
    <button on:click={() => deleteTodo(todo.id)}>X</button>
    <button on:click={() => openEditMode()}>edit</button>
  {/if}
</div>

<style>
  div {
    display: flex;
  }
</style>
