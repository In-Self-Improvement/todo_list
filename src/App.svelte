<script lang="ts">
  import Input from "./components/Input.svelte";
  import Todo from "./components/Todo.svelte";
  import Filter from "./components/Filter.svelte";

  let todo = ""; // input에 입력될 값!
  let todoList = [];
  let lastId = 0;
  let num = 0;
  // filter 추가
  let filterType = "All";
  let todoListStore = [];
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
      if (filterType !== "All") {
        todoListStore[todoListStore.length] = newTodo;
      }
    }
    setTimeout(() => {
      currentFilter(filterType);
    }, 1000);
  };

  // todo값을 업데이트 하면서, 엔터키를 누르면 할일이 추가되도록 하는 함수
  let handleKeyUp = (e) => {
    todo = e.target.value;
    if (e.keyCode === 13) {
      addTodo();
    }
  };
  let handleComplete = (id) => {
    // if (filterType !== "All") {
    //   const index = todoList.findIndex((todo) => todo.id === id);
    //   todoList[index]["completed"] = !todoList[index]["completed"];
    // }
    const index = todoList.findIndex((todo) => todo.id === id);
    console.log("com", index, todoList);
    todoList[index]["completed"] = !todoList[index]["completed"];
    selectedCount();
    setTimeout(() => {
      currentFilter(filterType);
    }, 1000);
  };
  let deleteTodo = (id) => {
    const todo = todoList.filter((todo) => todo.id !== id);
    const todoStore = todoListStore.filter((todo) => todo.id !== id);
    todoList = todo;
    if (filterType !== "All") {
      todoListStore = todoStore;
    }
    selectedCount();
  };
  let cancelEditTodo = (id, text) => {
    const index = todoList.findIndex((todo) => todo.id === id);
    todoList[index]["text"] = text;
    todoListStore[index]["text"] = text;
    selectedCount();
  };
  let editTodo = (id, text) => {
    if (filterType !== "All") {
      const index = todoListStore.findIndex((todo) => todo.id === id);
      todoListStore[index]["text"] = text;
    }
    const index = todoList.findIndex((todo) => todo.id === id);
    todoList[index]["text"] = text;
    selectedCount();
  };
  let selectedCount = () => {
    num = 0;
    todoList.forEach((todo) => {
      if (todo["completed"]) {
        num++;
      }
    });
  };
  let selectAllCompleted = () => {
    if (num === todoList.length) {
      for (let i = 0; i < todoList.length; i++) {
        todoList[i]["completed"] = false;
      }
      selectedCount();
      setTimeout(() => {
        currentFilter(filterType);
      }, 1000);
      return;
    }
    for (let i = 0; i < todoList.length; i++) {
      todoList[i]["completed"] = true;
    }
    selectedCount();
    setTimeout(() => {
      currentFilter(filterType);
    }, 1000);
  };
  let clearCompletedTodo = () => {
    const todoStore = todoListStore.filter((todo) => todo.completed !== true);
    todoListStore = todoStore;

    const todo = todoList.filter((todo) => todo.completed !== true);
    todoList = todo;

    selectedCount();
  };
  let filterAll = () => {
    if (todoListStore.length !== 0) {
      todoList = todoListStore;
    }
    filterType = "All";
    selectedCount();
  };
  let filterActive = () => {
    if (todoListStore.length === 0) {
      todoListStore = todoList;
    }
    todoList = todoListStore;
    const todo = todoList.filter((todo) => todo.completed !== true);
    todoList = todo;
    filterType = "Active";
    selectedCount();
  };
  let filterCompleted = () => {
    if (todoListStore.length === 0) {
      todoListStore = todoList;
    }
    todoList = todoListStore;
    const todo = todoList.filter((todo) => todo.completed === true);
    todoList = todo;
    filterType = "Completed";
    selectedCount();
  };
  let currentFilter = (filter: string) => {
    if (filter === "All") {
      filterAll();
    } else if (filter === "Active") {
      filterActive();
    } else if (filter === "Completed") {
      filterCompleted();
    }
  };
</script>

<main>
  <p>Todo list {num}{"/"}{todoList.length}</p>
  <Input
    {todo}
    {addTodo}
    {handleKeyUp}
    {selectAllCompleted}
    {clearCompletedTodo}
  />
  <Todo {todoList} {handleComplete} {deleteTodo} {editTodo} {cancelEditTodo} />
  <Filter {filterAll} {filterCompleted} {filterActive} {filterType} />
</main>

<style>
</style>
