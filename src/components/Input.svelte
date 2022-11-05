<script>
  export let todo;
  export let addTodo;
  export let handleKeyUp;
  export let selectAllCompleted;
  export let clearCompletedTodo;
</script>

<div>
  <input
    type="text"
    placeholder="할일을 입력하세요"
    bind:value={todo}
    on:keyup={(e) => handleKeyUp(e)}
  />
  <button on:click={addTodo}>ADD</button>
  <button on:click={selectAllCompleted}>ALL</button>
  <button on:click={clearCompletedTodo}>CLEAR</button>
</div>
