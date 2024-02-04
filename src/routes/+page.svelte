<script lang="ts">
  // STATE
  let todoText = "";
  let editedTodoId: null | number;
  let todos = [
    { id: 0, text: "an item", finished: false },
    { id: 1, text: "Second item", finished: false },
    { id: 2, text: "A third item too", finished: false },
  ];

  // HELPER FUNCS
  const resetTodoInput = () => {
    editedTodoId = null;
    todoText = "";
  };

  // EVENTS
  const clickOnSaveTodo = () => {
    if (typeof editedTodoId === "number") {
      todos.find((t) => t.id === editedTodoId)!.text = todoText;
      todos = todos;
    } else {
      todos = [
        ...todos,
        { id: todos.length + 1, text: todoText, finished: false },
      ];
    }

    resetTodoInput();
  };
  const clickOnTodo = (id: number) => {
    todos = todos.map((todo) => {
      if (todo.id === id) {
        todo.finished = !todo.finished;
      }

      return todo;
    });
  };
  const clickOnDeleteTodo = (id: number) => {
    if (
      confirm(
        `Do you really want to delete "${
          todos.find((t) => t.id === id)?.text
        }"?`
      )
    ) {
      todos = todos.filter((t) => t.id !== id);

      if (editedTodoId === id) {
        resetTodoInput();
      }
    }
  };
  const clickOnEditTodo = (id: number) => {
    editedTodoId = id;
    todoText = todos.find((t) => t.id === id)!.text;
  };
</script>

<div class="container">
  <h1>Todos with Svelte</h1>

  <div class="input-group mb-3">
    <input
      type="text"
      class="form-control"
      placeholder="Todo"
      aria-label="Todo"
      bind:value={todoText}
    />
    <button class="btn btn-primary" type="button" on:click={clickOnSaveTodo}>
      <i class="fa-solid fa-floppy-disk"></i>
    </button>
  </div>

  <ul class="list-group">
    {#each todos as todo}
      <!-- svelte-ignore a11y-click-events-have-key-events -->
      <!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
      <li class="list-group-item" on:click={() => clickOnTodo(todo.id)}>
        <span>
          <input type="checkbox" bind:checked={todo.finished} />
          {todo.text}
        </span>

        <span class="todo-operations">
          <!-- svelte-ignore a11y-no-static-element-interactions -->
          <i
            class="fa-solid fa-trash text-danger"
            on:click|stopPropagation={() => clickOnDeleteTodo(todo.id)}
          ></i>

          <!-- svelte-ignore a11y-no-static-element-interactions -->
          <i
            class="fa-solid fa-pencil text-warning"
            on:click|stopPropagation={() => clickOnEditTodo(todo.id)}
          ></i>
        </span>
      </li>
    {/each}
  </ul>
</div>

<style>
  h1 {
    font-size: 3rem;
    font-family: "Roboto";
  }

  .container {
    max-width: 500px;
  }

  .list-group-item {
    display: flex;
    gap: 10px;
    justify-content: space-between;
  }

  .todo-operations {
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .todo-operations i {
    cursor: pointer;
  }
</style>
