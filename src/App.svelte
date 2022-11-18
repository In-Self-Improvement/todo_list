<script lang="ts">
  import Input from "./components/Input.svelte";
  import Todo from "./components/Todo.svelte";
  import Filter from "./components/Filter.svelte";

  let todo = ""; // input에 입력될 값!
  let todoList = [];
  let filteredTodoList = [];
  let filterType = "All";
  let lastId = 0;
  let num = 0;
  // 할일을 추가하는 함수
  let addTodo = () => {
    if (todoList.length > 0) {
      lastId = todoList[todoList.length - 1]["id"];
    }
    if (todo) {
      let newTodo = {
        id: ++lastId,
        text: todo,
        completed: false,
      };

      todoList[todoList.length] = newTodo;
      todo = "";
    }
    console.log(todoList);
    currentFilter();
  };

  // todo값을 업데이트 하면서, 엔터키를 누르면 할일이 추가되도록 하는 함수
  let handleKeyUp = (e) => {
    todo = e.target.value;
    if (e.keyCode === 13) {
      addTodo();
    }
  };
  let handleComplete = (id) => {
    const index = todoList.findIndex((todo) => todo.id === id);
    todoList[index]["completed"] = !todoList[index]["completed"];
    currentFilter();
  };
  let deleteTodo = (id) => {
    const todo = todoList.filter((todo) => todo.id !== id);
    todoList = todo;
    currentFilter();
  };
  let cancelEditTodo = (id, text) => {
    const index = todoList.findIndex((todo) => todo.id === id);
    todoList[index]["text"] = text;
    selectedCount();
  };
  let editTodo = (id, text) => {
    const index = todoList.findIndex((todo) => todo.id === id);
    todoList[index]["text"] = text;
    selectedCount();
  };
  let selectedCount = () => {
    num = 0;
    todoList.forEach((todo) => {
      if (todo["completed"] === true) {
        num++;
      }
    });
    // for (let i = 0; i < todoList.length; i++) {
    //   if (todoList[i].completed === true) {
    //     num++;
    //   }
    // }
  };
  let selectAllCompleted = () => {
    if (filterType !== "All") {
      if (num === filteredTodoList.length) {
        for (let i = 0; i < filteredTodoList.length; i++) {
          filteredTodoList[i]["completed"] = false;
        }
        currentFilter();
        return;
      }
      for (let i = 0; i < filteredTodoList.length; i++) {
        filteredTodoList[i]["completed"] = true;
      }
    } else {
      if (num === todoList.length) {
        for (let i = 0; i < todoList.length; i++) {
          todoList[i]["completed"] = false;
        }
        currentFilter();
        return;
      }
      for (let i = 0; i < todoList.length; i++) {
        todoList[i]["completed"] = true;
      }
    }

    currentFilter();
  };
  let clearCompletedTodo = () => {
    const todo = todoList.filter((todo) => todo.completed !== true);
    todoList = todo;
    filteredTodoList = todo;

    currentFilter();
  };
  let filterAll = () => {
    filterType = "All";
  };
  let filterActive = () => {
    filterType = "Active";
    const todo = todoList.filter((todo) => todo.completed !== true);
    filteredTodoList = todo;
    console.log("Actice", filteredTodoList, filterType);
  };
  let filterCompleted = () => {
    filterType = "Completed";
    const todo = todoList.filter((todo) => todo.completed === true);
    filteredTodoList = todo;
    console.log("Completed", filteredTodoList, filterType);
  };
  let currentFilter = () => {
    if (filterType === "All") {
      filterAll();
    } else if (filterType === "Active") {
      filterActive();
    } else if (filterType === "Completed") {
      filterCompleted();
    }
    selectedCount();
    console.log("current filter", filterType, filteredTodoList, todoList);
  };
</script>

<main>
  {#if filterType !== "All"}
    <p>Todo list {num}{"/"}{filteredTodoList.length}</p>
  {:else}
    <p>Todo list {num}{"/"}{todoList.length}</p>
  {/if}
  <Input
    {todo}
    {addTodo}
    {handleKeyUp}
    {selectAllCompleted}
    {clearCompletedTodo}
  />
  <Todo
    {todoList}
    {handleComplete}
    {deleteTodo}
    {editTodo}
    {cancelEditTodo}
    {filteredTodoList}
    {filterType}
  />
  <Filter {filterAll} {filterCompleted} {filterActive} {filterType} />
</main>

<style>
</style>
