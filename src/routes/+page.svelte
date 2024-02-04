<div class="container">
  <h1>Todos with Svelte</h1>

  <div class="input-group mb-3">
    <input
      type="text"
      class="form-control"
      placeholder="Todo"
      aria-label="Todo"
    />
    <button class="btn btn-primary" type="button">
      <i class="fa-solid fa-floppy-disk"></i>
    </button>
  </div>

  <ul class="list-group">
    <li class="list-group-item">
      <input type="checkbox" /> An item
    </li>
    <li class="list-group-item">
      <input type="checkbox" /> A second item
    </li>
    <li class="list-group-item">
      <input type="checkbox" /> A third item
    </li>
    <li class="list-group-item">
      <input type="checkbox" /> A fourth item
    </li>
    <li class="list-group-item">
      <input type="checkbox" /> And a fifth one
    </li>
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
  }
</style>
