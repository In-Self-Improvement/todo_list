<script lang="ts">
  import Input from "./components/Input.svelte";
  import Todo from "./components/Todo.svelte";

  let todo = ""; // input에 입력될 값!
  let todoList = [];
  let lastId = 0;
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
  };
  let deleteTodo = (id) => {
    const todo = todoList.filter((todo) => todo.id !== id);
    todoList = todo;
  };
  let cancelEditTodo = (id, text) => {
    const index = todoList.findIndex((todo) => todo.id === id);
    todoList[index]["text"] = text;
  };
  let editTodo = (id, text) => {
    const index = todoList.findIndex((todo) => todo.id === id);
    todoList[index]["text"] = text;
  };
</script>

<main>
  <p>Todo list</p>
  <Input {todo} {addTodo} {handleKeyUp} />
  <Todo {todoList} {handleComplete} {deleteTodo} {editTodo} {cancelEditTodo} />
</main>

<style>
</style>
